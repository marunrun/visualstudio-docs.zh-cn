---
title: 属性的属性在 UML 类图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.logicalclassdiagram.attribute.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: ba01e064-7424-4e72-98fa-42fa1c30e153
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 24575f125c07a016bef4742e010cbdd51f6c75e9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154867"
---
# <a name="properties-of-attributes-on-uml-class-diagrams"></a>UML 类图上特性的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 类图上，你可以向类和接口添加 *特性* 。 特性用于定义可以附加到类实例或接口实例的值。  

 若要添加特性，请右键单击类或接口，指向“添加”  ，然后单击“特性”  。  

 如果看不到关系图上某个类的特性，请单击该类或接口顶部的 V 形来展开它。 如果可以看到“特性”  标题，则单击“[+]”  以展开特性部分。  

## <a name="signature-of-an-attribute"></a>特性的签名  
 特性的签名是在 UML 类图上的类或接口中表示该特性的行。 其格式如下：  

```  
+ AttributeName : TypeName [*]  
```  

 \+ 表示公共可见性。 其他允许的值为 - (private)、# (protected) 和 ~ (package)。  

 如果特性是静态的，则 `AttributeName` 带下划线。  

 如果特性没有类型，则省略 `: TypeName`。  

 `[*]` 表示重数。 如果重数为 1，则省略它。  

## <a name="properties"></a>属性  
 下表介绍 UML 类图上类或接口中的特性的属性。  

 若要查看某个特性的属性，请右键单击关系图上相应类或接口中的该特性，然后单击“属性”  。 这些属性将显示在“属性”窗口中。  

 若要查看某个特性的属性，请右键单击该特性，然后单击“属性”  。  

|   **Property**    | **默认**  |                                                                                                                                                                                                         描述                                                                                                                                                                                                          |
|-------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **默认值** |   （空）    |                                                                                                                                                                               实例化分类器时特性的值。                                                                                                                                                                                |
| **是只读的**  |    False     |                                                                                                                                                                                    如果为 True，则无法更改特性的值。                                                                                                                                                                                    |
|   **是静态的**   |    False     |                                                                                                                    如果为 True，则此特性的单个值在此类型的所有实例之间共享。<br /><br /> 如果为 True，则此特性的名称在关系图上显示时带有下划线。                                                                                                                    |
|     **名称**      | （新名称） |                                                                                                                                                                                        在所属分类器中应该是唯一的。                                                                                                                                                                                        |
|     **Type**      |    (无)    |                                                基元类型（如“整数”  ），或在模型中定义的类型。 你不能使用非基元类型（例如“十进制”  ），因为该值必须在元数据中编码。 如果在该属性中为新类型输入一个名称，将会向 UML 模型资源管理器的 **“未指定的类型”** 部分添加一个类型。                                                 |
|  **可见性**   |    Public    |                                     允许的值以及签名中显示的字符如下所示：<br /><br /> “”  - 全局可见<br /><br /> “”  - 对所属类型以外的类型不可见<br /><br /> “”  - 对派生自所有者的类型可见<br /><br /> “”  - 对同一包中的其他类型可见。                                      |
|  **工作项**   | 0 associated |                                                                                                                          关联工作项的计数。 只读。<br /><br /> 有关详细信息，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。                                                                                                                           |
|    **是叶**    |    False     |                                                                                                                                                                    如果为 True，则不允许在派生类型中重新定义此特性。                                                                                                                                                                     |
|  **派生**   |    False     |                                                                                                              如果为 True，则从其他特性计算此特性。 例如，从宽度和高度计算的对角线。 应在“描述”  或附加“注释”中写入详细信息。                                                                                                              |
|  **说明**  |   （空）    |                                                                                                                                                                        用于一般说明，或用于对特性中的值定义约束。                                                                                                                                                                        |
| **重数**  |      1       | “1”  - 此特性具有指定类型的一个值。<br /><br /> “”  - 此特性可具有 `null`值。<br /><br /> **\\** \* -此特性的值是值的集合。<br /><br /> **1..\\**  \* -此特性的值是包含至少一个值的集合。<br /><br /> *n* **..** *m* - 此特性的值是一个集合，它包含介于 *n* 和 *m* 之间的值。 |
|  **有序**   |    False     |                                                                                                                                                                    如果为 True，则集合构成一个顺序列表。 用于“重数”大于 1 的情况  。                                                                                                                                                                     |
|   **是唯一的**   |    False     |                                                                                                                                                                如果为 True，则集合中没有重复值。 用于“重数”大于 1 的情况  。                                                                                                                                                                |

## <a name="see-also"></a>请参阅  
 [UML 类关系图：引用](../modeling/uml-class-diagrams-reference.md)   
 [UML 类图上类型的属性](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [UML 类图上的操作的属性](../modeling/properties-of-operations-on-uml-class-diagrams.md)   
 [UML 类关系图：指导原则](../modeling/uml-class-diagrams-guidelines.md)   
 [UML 类关系图：指南](../modeling/uml-class-diagrams-guidelines.md)
