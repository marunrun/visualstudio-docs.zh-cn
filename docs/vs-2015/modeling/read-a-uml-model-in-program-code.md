---
title: 在程序代码中读取 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, reading models
ms.assetid: 0f63105e-6079-498a-94f1-318c0f5f9621
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bbc55204987f4b6ea0d45c4228f6c194f1ebaf64
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671307"
---
# <a name="read-a-uml-model-in-program-code"></a>在程序代码中读取 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 UML API 加载 UML 模型及其关系图。

## <a name="Reading"></a>在程序代码中读取模型
 若要访问模型的内容而不将其显示在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 窗口中，请使用 `ModelingProject.LoadReadOnly()`。

 例如:

```
using Microsoft.VisualStudio.Uml.Classes;
               // for IElement
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
               // for ModelingProject
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
               // for IModelStore
...
string projectPath = @"C:\MyProjectFolder\MyProject.modelproj";
using (IModelingProjectReader projectReader =
           ModelingProject.LoadReadOnly(projectPath))
{
   IModelStore store = projectReader.Store;
   foreach (IClass umlClass in store.AllInstances<IClass>())
   {
       ...
   }
}
```

 如果你想要读取关系图中的形状，则必须读取该项目，然后再读取该关系图。

 例如:

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
                             // for IDiagram
...
foreach (string diagramFile in projectReader. DiagramFileNames)
{
  IDiagram diagram = projectReader.LoadDiagram(diagramFile);
  foreach (IShape<IElement> shape
         in diagram.GetChildShapes<IElement>())
  { ... }
}
```

## <a name="alternative-methods"></a>替代方法
 对于许多应用程序而言，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Modelbus 允许您引用其中的模型和元素，这比本主题中所述的方法更可靠、更具灵活性。 它提供了一种在任意元素之间建立链接的标准方法，不论模型是否相同。 有关详细信息，请参阅将[UML 模型与其他模型和工具集成](../modeling/integrate-uml-models-with-other-models-and-tools.md)。

 你还可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API，在用户界面打开模型和关系图。 有关详细信息，请参阅[使用 Visual STUDIO API 打开 UML 模型](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)。

## <a name="Standalone"></a>独立应用程序
 上一节中的示例将用于 Visual Studio 扩展。 可以在独立的应用程序中读取模型，但你必须向 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目添加一些引用。

> [!NOTE]
> 有关在独立的应用程序中读取模型的方法的详细信息可能会在该产品的将来版本中进行更改。 当前版本中可以访问的一些功能可能在未来版本不会提供。

#### <a name="to-add-references-to-read-a-model-in-a-stand-alone-application"></a>添加引用以读取独立的应用程序中的模型。

1. 在解决方案资源管理器中，右键单击要在其中生成应用程序的项目，然后单击 "**属性**"。 在 "属性编辑器" 的 "**应用程序**" 选项卡中，将 "**目标框架**" 设置为所需的 .NET Framework 版本。

2. 添加你访问 UML 模型所需的 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 引用，通常为：

   - Microsoft.VisualStudio.Uml.Interfaces.dll

   - Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll

3. 除了前面部分中列出的引用外，还可以从 **\Program Files\Microsoft Visual Studio [version] \Common7\IDE\PrivateAssemblies**添加以下项目引用：

   - Microsoft.VisualStudio.Uml.dll

   - Microsoft.VisualStudio.TeamArchitect.ModelStore.Dsl.dll

     如果你想要读取应用程序中的关系图，你可能还需要这些引用：

   - Microsoft.VisualStudio.TeamArchitect.ActivityDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.ComponentDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.LogicalClassDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.SequenceDesigner.Dsl.dll

   - Microsoft.VisualStudio.TeamArchitect.UseCase.Dsl.dll

## <a name="see-also"></a>请参阅
 [用 UML API 编程](../modeling/programming-with-the-uml-api.md)[扩展 uml 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
