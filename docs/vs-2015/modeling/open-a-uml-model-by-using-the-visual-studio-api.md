---
title: 使用 Visual Studio API 打开 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, opening models in Visual Studio
ms.assetid: 38423682-f2a7-4d2a-a2cd-fd680e9b4b4d
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 694f10fb0af440513331aa6e76dbf9a59a16d340
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668510"
---
# <a name="open-a-uml-model-by-using-the-visual-studio-api"></a>使用 Visual Studio API 打开 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你还可以通过使用 API，在 Visual Studio 用户界面打开模型和关系图。

 如果你只想读取程序代码中的模型而不使其对用户可见，你可以使用以下方法：

- Visual Studio 模型总线允许你访问他们中的模型和元素，并提供一种在模型间建立连接的标准方法。 有关详细信息，请参阅将[UML 模型与其他模型和工具集成](../modeling/integrate-uml-models-with-other-models-and-tools.md)。

- 你可以在只读模式下打开某个模型。 有关详细信息，请参阅[在程序代码中读取 UML 模型](../modeling/read-a-uml-model-in-program-code.md)。

## <a name="Showing"></a>在 Visual Studio 中打开模型和关系图
 若要在用户界面中打开某个模型，请使用标准 Visual Studio API `EnvDTE.DTE`。 有两个有用的强制转换，你可以在建模项目项上执行：

- 如果项目是建模项目，并且已在当前 AppDomain 中加载该项目，则 `EnvDTE.Project` 可以在 `IModelingProject` 间来回转换。

- 如果该项为 UML 关系图，则 `EnvDTE.ProjectItem` 可以在 `IDiagramContext` 间来回转换。

  对于以下示例，你的项目应导入这些引用：

- EnvDTE

- Microsoft.VisualStudio.ArchitectureTools.Extensibility

- Microsoft.VisualStudio.Modeling.Sdk.[版本号]

- Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]

- Microsoft.VisualStudio.Shell.Immutable.[版本号]

- Microsoft.VisualStudio.Uml.Interfaces

- System.ComponentModel.Composition

  示例将在 Visual Studio 中打开一个 UML 模型：

```
using EnvDTE; // Visual Studio API for loading diagrams
using
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   // for ICommandExtension and other handler types
using Microsoft.VisualStudio.Uml.Classes;
   // for basic UML types
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   // for model construction methods
using EnvDTE;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
                             // for IDiagram
...
```

 在 Visual Studio 扩展中，你可以做出此声明，以获取对主机服务提供程序的访问权限：

```
[Import] public Microsoft.VisualStudio.Shell.SVsServiceProvider ServiceProvider {get;set;}
...
```

 在方法中，你可以访问项目，例如，当前的项目：

```
DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
Project project = dte.ActiveDocument.ProjectItem.ContainingProject;
IModelingProject modelingProject = project as IModelingProject;
if (modelingProject == null) return; // not a modeling project

// Access the model's store and contents.
IModelStore store = modelingProject.Store;
foreach (IElement element in store.Root.OwnedElements) {...}

// Open all the project's diagrams.
foreach (ProjectItem item in project.ProjectItems)
{
     IDiagramContext modelingItem = item as IDiagramContext;
     if (modelingItem == null)
         continue; // not a model diagram
     IDiagram diagram = modelingItem.CurrentDiagram;
     if (diagram == null)
     {
        // Diagram is closed. Open it.
        item.Open().Activate();
        diagram = modelingItem.CurrentDiagram;
     }
     // Access the shapes.
     foreach (IShape<IElement> shape
               in diagram.GetChildShapes<IElement>())
     {
       IElement displayedElement = shape.Element;
       ...
     }
   }
}
```

## <a name="see-also"></a>请参阅
 [用 UML API 编程](../modeling/programming-with-the-uml-api.md)[扩展 uml 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
