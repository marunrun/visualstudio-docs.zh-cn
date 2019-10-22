---
title: UML 类图上的操作的属性 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67d752fa802deef5dcc40fdfa4d762dc6edb1d0d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671354"
---
# <a name="properties-of-operations-on-uml-class-diagrams"></a>UML 类图中操作的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 类图中，您可以向类和接口添加*操作*。 操作即一种可以由类或接口的实例执行的方法或函数。

 若要添加操作，请右键单击类或接口，指向 "**添加**"，然后单击 "**操作**"。

 如果图上类的操作不可见，则单击类或接口顶部的 V 形图标以将其展开。 如果可以看到**操作**标头，请单击 " **[+]** " 以展开 "操作" 部分。

## <a name="signature-of-an-operation"></a>操作的签名
 操作的签名是在 UML 类图上的类或接口中表示特性的文本的行。 它具有以下形式：

 \+ OperationName （parameter1： Type1 [*]，...）： ReturnType [\*]

 \+ 表示公共可见性。 其他允许的值为 - (private)、# (protected) 和 ~ (package)。

 如果**Is Static**属性为 true，则 `OperationName` 带有下划线，如果**is Abstract**属性为 true，则为斜体。

 如果没有已定义的返回类型，则省略 `: ReturnType`。

 `[*]` 表示参数或返回类型的重数。 如果重数为 1，则省略它。

 请参阅下节，了解这些属性的完整说明。

## <a name="properties"></a>属性
 UML 类图的类或接口中有操作的多个属性。

 若要查看某个操作的属性，请在关系图的类或接口中右键单击该操作，然后单击 "**属性**"。 属性将显示在 "**属性**" 窗口中。

|      Property       |   Default    |                                                                                                                                                                                 描述                                                                                                                                                                                 |
|---------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      **名称**       | （新名称） |                                                                                                                                                                在包含类型中为唯一。                                                                                                                                                                 |
|   **参数**    |    (无)    |      具有以下<em>格式的</em>**列表：** <em>type</em> **、** <em>name</em> **：** <em>type</em> **、...** 。 单击 " **[...]** " 以编辑列表。<br /><br /> 类型可以为基元类型，或是在模型中定义的类型。 如果在该属性中为新类型输入一个名称，将会向 UML 模型资源管理器的 **“未指定的类型”** 部分添加一个类型。      |
|   **返回类型**   |    (无)    |                                                                               **（无）** 、基元类型或模型中定义的类型。 如果在该属性中为新类型输入一个名称，将会向 UML 模型资源管理器的 **“未指定的类型”** 部分添加一个类型。                                                                                |
| **后**  |    (无)    |                                                                                                                         一个可选条件，指定执行操作前后系统状态之间的关系。                                                                                                                         |
|  **前提**  |    (无)    |                                                                                                                            一个可选条件，指定在开始执行操作之前，有关系统状态的假设。                                                                                                                            |
| **主体条件** |    (无)    |                                                                                                                                                       有关操作返回的值的可选约束。                                                                                                                                                       |
|   **可见性**    |    Public    |                  允许的值以及显示在签名中的字符如下所示：<br /><br /> “” - 全局可见<br /><br /> “” - 对所属类型以外的类型不可见<br /><br /> “” - 对派生自所有者的类型可见<br /><br /> “” - 对同一包中的其他类型可见。                   |
|    **信号**    |  +*名称*（）   |                                                                                      概述此操作的可见性、名称、参数和返回类型。 你可以通过编辑关系图上的签名或编辑单个属性来更改这些属性。                                                                                      |
|   **工作项**    | 0 associated |                                                                                                  关联工作项的计数。 只读。<br /><br /> 有关详细信息，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。                                                                                                  |
|   **并发**   |  顺序  | **顺序**-操作为或将设计为无并发控制。 同时调用此操作可能会导致失败。<br /><br /> **受保护**-此操作将自动被阻止，直到它的其他实例完成。<br /><br /> **并发**-设计该操作，以便对它的多个调用可以并发执行。 |
|    **为静态**    |    False     |                                                                                                  如果为 True，则此操作将在该类型的所有实例之间共享。<br /><br /> 如果为 True，则此操作的名称在关系图上显示时将带有下划线。                                                                                                   |
|   **是抽象的**   |    False     |                                                                                                                                        如果为 True，则没有与此操作相关联的代码。 因此，所属类是抽象类。                                                                                                                                         |
|     **为叶**     |    False     |                                                                                                                                              设计器设计为不能在派生类中重写此操作。                                                                                                                                              |
|    **为查询**     |    False     |                                                                                                 如果为 True，则此操作不会对系统状态进行重大更改。 因此，可以用在比如测试当中来检查系统状态。                                                                                                  |
|  **多样性**   |      1       |                                 **1** -指定类型的单个值。<br /><br /> **0 .0** -可以 `null`。<br /><br /> \*-指定类型的值的集合。<br /><br /> **1. \\** \*-包含至少一个值的集合。<br /><br /> *n* `..` *m* -包含 `n` 和 `m` 值之间的集合。                                  |
|   **已排序**    |    False     |                                                                                                                                             如果为 True，则集合构成一个顺序列表。 重**数**大于1。                                                                                                                                              |
|    **是唯一的**    |    False     |                                                                                                                                         如果为 True，则集合中没有重复值。 重**数**大于1。                                                                                                                                         |

## <a name="see-also"></a>请参阅
 [Uml 类图：引用](../modeling/uml-class-diagrams-reference.md)uml 类图上的[类型](../modeling/properties-of-types-on-uml-class-diagrams.md)的属性 uml 类图上[特性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)的属性 uml 类图上[关联](../modeling/properties-of-associations-on-uml-class-diagrams.md)的属性 uml 类图[：准则](../modeling/uml-class-diagrams-guidelines.md)
