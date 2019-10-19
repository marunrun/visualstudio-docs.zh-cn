---
title: UML 类图：引用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.common.generalization.properties
- vs.teamarch.logicalclassdiagram.toolbox
- vs.teamarch.UMLModelExplorer.association
- vs.teamarch.common.unspecifiedtype.properties
- vs.teamarch.logicalclassdiagram.diagram
- vs.teamarch.UMLModelExplorer.logicalclassdiagram
- vs.teamarch.UMLModelExplorer.generalization
- vs.teamarch.common.unspecifiedtype
helpviewer_keywords:
- UML diagrams, class
- diagrams - modeling, class
- UML, class diagrams
- class diagrams - UML
- diagrams - modeling, UML class
ms.assetid: b7c88be0-0d86-4d65-af74-f37e8812d20f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6d2368c19292f9e4205cec9f1b42b1553ce3188f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658442"
---
# <a name="uml-class-diagrams-reference"></a>UML 类图：参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 类图描述在应用程序内部以及应用程序与其用户在通信时使用的对象和信息结构。 它描述的信息不具有对任何特定实现的引用。 它的类和关系可以采用许多方法来实现，例如数据库表、XML 节点或软件对象的组合。

> [!NOTE]
> 本主题针对 UML 类图。 还有另一种类图，即 .NET 类图，它用于可视化程序代码。 有关详细信息，请参阅[设计和查看类和类型](http://go.microsoft.com/fwlink/?LinkId=142231)。

 若要创建 UML 类图，请在 "**体系结构**" 菜单上，选择 "**新建 UML 或层关系图**"。 有关如何绘制 UML 类图的详细信息，请参阅[Uml 类图：准则](../modeling/uml-class-diagrams-guidelines.md)。 有关如何创建和绘制建模图的详细信息，请参阅[编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="reading-class-diagrams"></a>读取类图
 本节中的表介绍可在 UML 类图上看到的元素。 有关这些元素的属性的信息，请参阅以下主题：

- [UML 类图上类型的属性](../modeling/properties-of-types-on-uml-class-diagrams.md)

- [UML 类图上特性的属性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML 类图中操作的属性](../modeling/properties-of-operations-on-uml-class-diagrams.md)

- [UML 类图上关联的属性](../modeling/properties-of-associations-on-uml-class-diagrams.md)

  ![显示关系和属性的三个类](../modeling/media/uml-classovreading.png "UML_ClassOvReading")

| **整形** |       **元素**        |                                                                                                                                                             **描述**                                                                                                                                                              |
|-----------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     1     |        **类**         |                                                           共享给定结构或行为特征的对象的定义。 有关详细信息，请参阅[UML 类图上类型的属性](../modeling/properties-of-types-on-uml-class-diagrams.md)。                                                            |
|     1     |        分类器        |                                                                                                             类、接口或枚举的通用名称。 组件、用例和参与者也是分类器。                                                                                                             |
|     2     | 折叠/展开控件 |                                                                                         如果看不到分类器的详细信息，则单击分类器左上角的扩展器。 可能还必须单击每段上的 [+]。                                                                                         |
|     3     |      **特性**       |   附加到每个分类器实例的类型化值。<br /><br /> 若要添加属性，请单击 "**属性**" 部分，然后按**enter**。 键入该特性的签名。 有关详细信息，请参阅[UML 类图上特性的属性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)。   |
|     4     |      **运作**       | 分类器的实例可执行的方法或函数。 若要添加操作，请单击 "**操作**" 部分，然后按**enter**。 键入该操作的签名。 有关详细信息，请参阅[UML 类图上的操作属性](../modeling/properties-of-operations-on-uml-class-diagrams.md)。 |
|     5     |     **关联**      |                                                                  两个分类器的成员之间的关系。 有关详细信息，请参阅[UML 类图上关联的属性](../modeling/properties-of-associations-on-uml-class-diagrams.md)。                                                                   |
|    5a     |     **聚合**      |                                                                                                    表示共享所有权关系的关联。 所有者角色的 "**聚合**" 属性设置为 "**共享**"。                                                                                                     |
|    5b     |     **组合**      |                                                                                                      表示整体-部分关系的关联。 所有者角色的 "**聚合**" 属性设置为 "**组合**"。                                                                                                      |
|     6     |   **关联名称**   |                                                                                                                                         关联的名称。 该名称可以留空。                                                                                                                                          |
|     7     |      **角色名称**       |                       角色（即关联的一端）的名称。 可用于引用关联对象。 在前面的图示中，对于任何“订单”`O`，`O.ChosenMenu` 是其关联菜单。<br /><br /> 每个角色都有自己的属性，这些属性列在关联的属性下。                       |
|     8     |     **多样性**     |                                         指示此端有多少个对象可以链接到另一端的每个对象。 在该示例中，每个“订单”必须链接到正好一个“菜单”。<br /><br /> **\\** \* 表示可以进行的链接数没有上限。                                         |
|     9     |    **泛**    |  *特定*分类器从*通用*分类器继承部分定义。 通用分类器位于连接线的箭头端。 特定分类器继承特性、关联和操作。<br /><br /> 使用 "**继承**" 工具在两个分类器之间创建泛化。   |

 ![包含接口和枚举的包](../modeling/media/uml-classovpackage.png "UML_ClassOvPackage")

|形状|元素|描述|
|-----------|-------------|-----------------|
|10|**Interface**|对象的部分外部可见行为的定义。 有关详细信息，请参阅[UML 类图上类型的属性](../modeling/properties-of-types-on-uml-class-diagrams.md)。|
|11|**枚举**|由一组文本值组成的分类器。|
|12|**包**|一组分类器、关联、操作、生命线、组件和包。 逻辑类图表示包中包含成员分类器和成员包。<br /><br /> 名称在包中的范围内，因此**Package1**中的**class1**不同于该包之外的**class1** 。 包的名称将显示为其内容的**限定名称**属性的一部分。<br /><br /> 可以设置任何 UML 关系图的**链接包**属性来引用包。 在该关系图上创建的所有元素随后都将成为该包的一部分。 它们将显示在 " **UML 模型资源管理器**" 中的包下。|
|13|**Import**|包之间的关系，指示一个包中包括另一个包的所有定义。|
|14|**依赖项**|如果箭头端的分类器发生更改，则依赖分类器的定义或实现可能会更改。|

 ![与连接器和棒糖形一起显示的实现](../modeling/media/uml-classovrealize.png "UML_ClassOvRealize")

|形状|**元素**|描述|
|-----------|-----------------|-----------------|
|15|**实现**|该类实现由接口定义的操作和特性。<br /><br /> 使用 "**继承**" 工具创建类和接口之间的实现。|
|16|**实现**|同一关系的可选表示形式。 棒糖形符号上的标签用于标识接口。<br /><br /> 若要创建此表示形式，请选择一个现有实现关系。 关联附近将显示一个操作标记。 单击操作标记，然后单击 "**显示为棒糖形**"。|

## <a name="see-also"></a>请参阅
 [编辑 uml 模型和关系图](../modeling/edit-uml-models-and-diagrams.md) [uml 类图：](../modeling/uml-class-diagrams-guidelines.md) uml 类图上[类型](../modeling/properties-of-types-on-uml-class-diagrams.md)的准则属性 uml 类图上[特性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)的属性 uml 类图上[的](../modeling/properties-of-operations-on-uml-class-diagrams.md)属性属性[UML 类图上的关联](../modeling/properties-of-associations-on-uml-class-diagrams.md)
