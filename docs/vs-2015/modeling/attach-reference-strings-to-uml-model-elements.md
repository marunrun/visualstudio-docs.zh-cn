---
title: 将引用字符串附加到 UML 模型元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- UML - extending, reference strings
ms.assetid: 15dbed99-efce-42fe-a768-714a5804e7d1
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bd5a1ae4abc2e0b5c508b7b77160bbf8da3bb45e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203229"
---
# <a name="attach-reference-strings-to-uml-model-elements"></a>将引用字符串附加到 UML 模型元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以编写代码以将任意字符串附加到模型元素。 例如，字符串可以是 URI、计算的缓存结果或对另一个模型中的某个元素的 ModelBus 引用。 每个字符串都包含在 IReference 对象中。 可以向各个模型元素附加任意数量的 IReference 对象。  
  
 每个 IReference 对象都有一个名称。 可以使用此名称指示如何解释引用值。 例如，你可以将名称设置为“URI”，以指示应将该值解释为 URI。 有一些被建模工具所使用的预定义引用名称值。  
  
## <a name="attaching-a-reference-to-an-ielement"></a>将引用附加到 IElement  
 若要使用以下方法，你必须将引用添加到：  
  
 Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll  
  
 你应在代码中插入此指令：  
  
 `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`  
  
|方法调用|描述|  
|-----------------|-----------------|  
|`element.AddReference (nameString, valueString, duplicatesAllowed)`|使用给定的名称和值字符串创建 `IReference`，并将其链接到 `element`。 返回 `IReference`。<br /><br /> 如果 `duplicatesAllowed` 为 False 并且已经有一个具有相同名称的 `IReference` 附加到 `element`，则会引发异常。|  
|`element.GetReferences(name)`|返回所有链接到具有给定的 `IReference` 的 `element` 的 `name` 对象。|  
|`element.DeleteAllReferences(name)`|删除所有链接到具有给定名称的元素的 `IReference` 对象。|  
|`reference.Delete()`|删除此 `IReference`。|  
|`ReferenceConstants.WorkItem`|用于命名工作项引用的值。|  
  
## <a name="see-also"></a>请参阅  
 [定义工作项链接处理程序](../modeling/define-a-work-item-link-handler.md)   
 [定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)   
 [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)
