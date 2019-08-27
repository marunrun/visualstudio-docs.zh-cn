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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a5f60338a8a856b4c6ef8fa913d6d7168ff67bb9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427028"
---
# <a name="get-uml-model-elements-from-idataobject"></a>从 IDataObject 获取 UML 模型元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用户将元素从任何源拖到关系图上时，在 `System.Windows.Forms.IDataObject` 中对拖动的元素进行编码。 编码取决于源对象的类型。 以下片段演示当源为 UML 关系图时如何检索元素。  
  
> [!NOTE]
> 可以使用类型执行的大多数操作，您只需在 UML 模型中定义的程序集中**Microsoft.VisualStudio.Uml.Interfaces**和**Microsoft.VisualStudio.ArchitectureTools.Extensibility**。 但是，出于此目的，你必须使用属于 UML 建模工具的实现的一些类。 例如，此片段中的 `ShapeElement` 与 UML `IShape` 并不相同。 为了降低将 UML 模型和关系图置于不一致状态的风险，最好避免使用这些实现类的方法，除非没有备用方法。  
  
## <a name="code-sample"></a>代码示例  
 你的项目必须引用以下[!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)]程序集：  
  
 **Microsoft.VisualStudio.Modeling.Sdk.[version]**  
  
 **Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]**  
  
 **System.Windows.Forms**  
  
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
  
 有关详细信息`ElementGroupPrototype`并`Store`中的 UML 建模工具的实现，请参阅[Visual Studio-域特定语言的建模 SDK](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)   
 [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
