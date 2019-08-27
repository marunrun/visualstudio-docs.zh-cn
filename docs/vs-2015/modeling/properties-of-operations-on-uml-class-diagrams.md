---
title: 类图的 uml 操作属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.logicalclassdiagram.operation.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: 4128f3e2-3a51-4edf-b3e4-b7f170a32f6b
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f98a3211bebf832009b84fac0fc1305a4162c610
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154823"
---
# <a name="properties-of-operations-on-uml-class-diagrams"></a>UML 类图中操作的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 类图中，您可以添加*操作*向类和接口。 操作即一种可以由类或接口的实例执行的方法或函数。  

 若要添加操作，请右键单击类或接口，指向**外**，然后单击**操作**。  

 如果图上类的操作不可见，则单击类或接口顶部的 V 形图标以将其展开。 如果您所见**操作**标头，单击 **[+]** 以展开操作部分。  

## <a name="signature-of-an-operation"></a>操作的签名  
 操作的签名是在 UML 类图上的类或接口中表示特性的文本的行。 它具有以下形式：  

 \+ OperationName (parameter1:Type1 [*]):ReturnType [\*]  

 \+ 表示公共可见性。 其他允许的值为 - (private)、# (protected) 和 ~ (package)。  

 `OperationName` 如果添加下划线**Is Static**属性为 true，并为斜体如果**Is Abstract**属性为 true。  

 如果没有已定义的返回类型，则省略 `: ReturnType`。  

 `[*]` 表示参数或返回类型的重数。 如果重数为 1，则省略它。  

 请参阅下节，了解这些属性的完整说明。  

## <a name="properties"></a>属性  
 UML 类图的类或接口中有操作的多个属性。  

 要查看操作的属性，请右键单击关系图中，在类或接口中的操作，然后单击**属性**。 属性将显示在**属性**窗口。  

|      Property       |   默认    |                                                                                                                                                                                 描述                                                                                                                                                                                 |
|---------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      **名称**       | （新名称） |                                                                                                                                                                在包含类型中为唯一。                                                                                                                                                                 |
|   **Parameters**    |    (无)    |      具有窗体的列表<em>名称</em> **:** <em>类型</em> **，** <em>名称</em> **:** <em>类型</em> **，...** 单击 **[...]** 编辑的列表。<br /><br /> 类型可以为基元类型，或是在模型中定义的类型。 如果在该属性中为新类型输入一个名称，将会向 UML 模型资源管理器的 **“未指定的类型”** 部分添加一个类型。      |
|   **返回类型**   |    (无)    |                                                                               **（无）** ，或基元类型或在模型中定义的类型。 如果在该属性中为新类型输入一个名称，将会向 UML 模型资源管理器的 **“未指定的类型”** 部分添加一个类型。                                                                                |
| **后置条件**  |    (无)    |                                                                                                                         一个可选条件，指定执行操作前后系统状态之间的关系。                                                                                                                         |
|  **前置条件**  |    (无)    |                                                                                                                            一个可选条件，指定在开始执行操作之前，有关系统状态的假设。                                                                                                                            |
| **正文条件** |    (无)    |                                                                                                                                                       有关操作返回的值的可选约束。                                                                                                                                                       |
|   **可见性**    |    Public    |                  允许的值以及显示在签名中的字符如下所示：<br /><br /> “”  - 全局可见<br /><br /> “”  - 对所属类型以外的类型不可见<br /><br /> “”  - 对派生自所有者的类型可见<br /><br /> “”  - 对同一包中的其他类型可见。                   |
|    **签名**    |  +*名称*（)   |                                                                                      概述此操作的可见性、名称、参数和返回类型。 你可以通过编辑关系图上的签名或编辑单个属性来更改这些属性。                                                                                      |
|   **工作项**    | 0 associated |                                                                                                  关联工作项的计数。 只读。<br /><br /> 有关详细信息，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。                                                                                                  |
|   **并发**   |  顺序  | **顺序**-或该操作将不进行并发控制而设计。 同时调用此操作可能会导致失败。<br /><br /> **受保护的**-它的其他实例完成之前，将自动阻止该操作。<br /><br /> **并发**-操作的因此可以并发执行多个调用。 |
|    **是静态的**    |    False     |                                                                                                  如果为 True，则此操作将在该类型的所有实例之间共享。<br /><br /> 如果为 True，则此操作的名称在关系图上显示时将带有下划线。                                                                                                   |
|   **是抽象的**   |    False     |                                                                                                                                        如果为 True，则没有与此操作相关联的代码。 因此，所属类是抽象类。                                                                                                                                         |
|     **是叶**     |    False     |                                                                                                                                              设计器设计为不能在派生类中重写此操作。                                                                                                                                              |
|    **是查询**     |    False     |                                                                                                 如果为 True，则此操作不会对系统状态进行重大更改。 因此，可以用在比如测试当中来检查系统状态。                                                                                                  |
|  **重数**   |      1       |                                 **1** -指定类型的单个值。<br /><br /> **0..1** -可以是`null`。<br /><br /> \* -指定类型的值的集合。<br /><br /> **1..\\**  \* -包含至少一个值的集合。<br /><br /> *n* `..` *m*的集合，其中包含之间`n`和`m`值。                                  |
|   **有序**    |    False     |                                                                                                                                             如果为 True，则集合构成一个顺序列表。 有关**多重性**大于 1。                                                                                                                                              |
|    **是唯一的**    |    False     |                                                                                                                                         如果为 True，则集合中没有重复值。 有关**多重性**大于 1。                                                                                                                                         |

## <a name="see-also"></a>请参阅  
 [UML 类关系图：引用](../modeling/uml-class-diagrams-reference.md)   
 [UML 类图上类型的属性](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [UML 类图上特性的属性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)   
 [UML 类图上关联的属性](../modeling/properties-of-associations-on-uml-class-diagrams.md)   
 [UML 类关系图：指南](../modeling/uml-class-diagrams-guidelines.md)
