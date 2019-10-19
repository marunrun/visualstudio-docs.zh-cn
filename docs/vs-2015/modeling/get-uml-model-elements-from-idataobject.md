---
title: 从 IDataObject 获取 UML 模型元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, copy and paste
ms.assetid: e0b9cec8-3b93-4a24-8bd3-3e086501d387
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 66b4ffc312af89aa5852a1f4dad62fd328176df3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666076"
---
# <a name="get-uml-model-elements-from-idataobject"></a>从 IDataObject 获取 UML 模型元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用户将元素从任何源拖到关系图上时，在 `System.Windows.Forms.IDataObject` 中对拖动的元素进行编码。 编码取决于源对象的类型。 以下片段演示当源为 UML 关系图时如何检索元素。

> [!NOTE]
> 您必须对 UML 模型执行的大部分操作都可以通过使用程序集**VisualStudio**和**VisualStudio**中定义的类型来执行的操作来执行。 但是，出于此目的，你必须使用属于 UML 建模工具的实现的一些类。 例如，此片段中的 `ShapeElement` 与 UML `IShape` 并不相同。 为了降低将 UML 模型和关系图置于不一致状态的风险，最好避免使用这些实现类的方法，除非没有备用方法。

## <a name="code-sample"></a>代码示例
 你的项目必须引用以下 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 程序集：

 **VisualStudio 的。版本**

 **VisualStudio 的关系图。版本**

 **System.web. Forms**

```
using Microsoft.VisualStudio.Modeling;
  // for ElementGroupPrototype
using Microsoft.VisualStudio.Modeling.Diagrams;
  // for ShapeElement, DiagramDragEventArgs, DiagramPointEventArgs
… 
  /// <summary>
  /// Retrieves UML IElements from drag arguments.
  /// Works for drags from UML diagrams.
  /// </summary>
  private IEnumerable<IElement> GetModelElementsFromDragEvent
                  (DiagramDragEventArgs dragEvent)
  {
     //ElementGroupPrototype is the container for
     //dragged and copied elements and toolbox items.
     ElementGroupPrototype prototype =
        dragEvent.Data.
        GetData(typeof(ElementGroupPrototype))
                     as ElementGroupPrototype;
     // Locate the originals in the implementation store.
     IElementDirectory implementationDirectory =
        dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;

     return  prototype.ProtoElements.Select(
       prototypeElement =>
       {
          ModelElement element = implementationDirectory
                .FindElement(prototypeElement.ElementId);
          ShapeElement shapeElement = element as ShapeElement;
          if (shapeElement != null)
          {
            // Dragged from a diagram.
            return shapeElement.ModelElement as IElement;
          }
          else
          {
            // Dragged from UML Model Explorer.
            return element as IElement;
          }
        });
    }
```

 有关 `ElementGroupPrototype` 和实现 UML 建模工具的 `Store` 的详细信息，请参阅[用于 Visual Studio 的建模 SDK-特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)。

## <a name="see-also"></a>请参阅
 [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)在[建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
