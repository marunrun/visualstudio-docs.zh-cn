---
title: 'UML Class Diagrams: Reference | Microsoft Docs'
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
ms.openlocfilehash: da4e0e3bab904b660f3d843e105b7d256a63a1b5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297224"
---
# <a name="uml-class-diagrams-reference"></a>UML 类图：参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 类图描述在应用程序内部以及应用程序与其用户在通信时使用的对象和信息结构。 它描述的信息不具有对任何特定实现的引用。 它的类和关系可以采用许多方法来实现，例如数据库表、XML 节点或软件对象的组合。

> [!NOTE]
> 本主题针对 UML 类图。 还有另一种类图，即 .NET 类图，它用于可视化程序代码。 For more information, see [Designing and Viewing Classes and Types](https://go.microsoft.com/fwlink/?LinkId=142231).

 To create a UML class diagram, on the **Architecture** menu, choose **New UML or Layer Diagram**. For more information about how to draw UML class diagrams, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md). For more information about how to create and draw modeling diagrams, see [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="reading-class-diagrams"></a>读取类图
 本节中的表介绍可在 UML 类图上看到的元素。 有关这些元素的属性的信息，请参阅以下主题：

- [UML 类图上类型的属性](../modeling/properties-of-types-on-uml-class-diagrams.md)

- [UML 类图上特性的属性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML 类图中操作的属性](../modeling/properties-of-operations-on-uml-class-diagrams.md)

- [UML 类图上关联的属性](../modeling/properties-of-associations-on-uml-class-diagrams.md)

  ![Three classes showing relationships and properties](../modeling/media/uml-classovreading.png "UML_ClassOvReading")

| **Shape** |       **元素**        |                                                                                                                                                             **描述**                                                                                                                                                              |
|-----------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     1     |        **类**         |                                                           共享给定结构或行为特征的对象的定义。 For more information, see [Properties of types on UML class diagrams](../modeling/properties-of-types-on-uml-class-diagrams.md).                                                            |
|     1     |        分类器        |                                                                                                             类、接口或枚举的通用名称。 组件、用例和参与者也是分类器。                                                                                                             |
|     2     | 折叠/展开控件 |                                                                                         如果看不到分类器的详细信息，则单击分类器左上角的扩展器。 可能还必须单击每段上的 [+]。                                                                                         |
|     3     |      **特性**       |   附加到每个分类器实例的类型化值。<br /><br /> To add an attribute, click the **Attributes** section and then press **ENTER**. 键入该特性的签名。 For more information, see [Properties of attributes on UML class diagrams](../modeling/properties-of-attributes-on-uml-class-diagrams.md).   |
|     4     |      **Operation**       | 分类器的实例可执行的方法或函数。 To add an operation, click the **Operations** section and then press **ENTER**. 键入该操作的签名。 For more information, see [Properties of operations on UML class diagrams](../modeling/properties-of-operations-on-uml-class-diagrams.md). |
|     5     |     **Association**      |                                                                  两个分类器的成员之间的关系。 For more information, see [Properties of associations on UML class diagrams](../modeling/properties-of-associations-on-uml-class-diagrams.md).                                                                   |
|    5a     |     **聚合**      |                                                                                                    表示共享所有权关系的关联。 The **Aggregation** property of the owner role is set to **Shared**.                                                                                                     |
|    5b     |     **Composition**      |                                                                                                      表示整体-部分关系的关联。 The **Aggregation** property of the owner role is set to **Composite**.                                                                                                      |
|     6     |   **Association Name**   |                                                                                                                                         关联的名称。 该名称可以留空。                                                                                                                                          |
|     7     |      **Role Name**       |                       角色（即关联的一端）的名称。 可用于引用关联对象。 在前面的图示中，对于任何“订单”`O`，`O.ChosenMenu` 是其关联菜单。<br /><br /> 每个角色都有自己的属性，这些属性列在关联的属性下。                       |
|     8     |     **Multiplicity**     |                                         指示此端有多少个对象可以链接到另一端的每个对象。 在该示例中，每个“订单”必须链接到正好一个“菜单”。<br /><br /> **\\** \* means that there is no upper limit to the number of links that can be made.                                         |
|     9     |    **Generalization**    |  The *specific* classifier inherits part of its definition from the *general* classifier. 通用分类器位于连接线的箭头端。 特定分类器继承特性、关联和操作。<br /><br /> Use the **Inheritance** tool to create a generalization between two classifiers.   |

 ![Package containing interface and enumeration](../modeling/media/uml-classovpackage.png "UML_ClassOvPackage")

|形状|元素|描述|
|-----------|-------------|-----------------|
|10|**Interface**|对象的部分外部可见行为的定义。 For more information, see [Properties of types on UML class diagrams](../modeling/properties-of-types-on-uml-class-diagrams.md).|
|11|**Enumeration**|由一组文本值组成的分类器。|
|12|**包**|一组分类器、关联、操作、生命线、组件和包。 逻辑类图表示包中包含成员分类器和成员包。<br /><br /> Names are scoped within packages so that **Class1** within **Package1** is distinct from **Class1** outside that package. The name of the package appears as part of the **Qualified Name** properties of its contents.<br /><br /> You can set the **Linked Package** property of any UML diagram to refer to a package. 在该关系图上创建的所有元素随后都将成为该包的一部分。 They will appear under the package in **UML Model Explorer**.|
|13|**Import**|包之间的关系，指示一个包中包括另一个包的所有定义。|
|14|**Dependency**|如果箭头端的分类器发生更改，则依赖分类器的定义或实现可能会更改。|

 ![Realization shown with conector and lollipop](../modeling/media/uml-classovrealize.png "UML_ClassOvRealize")

|形状|**元素**|描述|
|-----------|-----------------|-----------------|
|15|**Realization**|该类实现由接口定义的操作和特性。<br /><br /> Use the **Inheritance** tool to create a realization between a class and an interface.|
|16|**Realization**|同一关系的可选表示形式。 棒糖形符号上的标签用于标识接口。<br /><br /> 若要创建此表示形式，请选择一个现有实现关系。 关联附近将显示一个操作标记。 Click the action tag, and then click **Show as Lollipop**.|

## <a name="see-also"></a>请参阅
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md) [Properties of types on UML class diagrams](../modeling/properties-of-types-on-uml-class-diagrams.md) [Properties of attributes on UML class diagrams](../modeling/properties-of-attributes-on-uml-class-diagrams.md) [Properties of operations on UML class diagrams](../modeling/properties-of-operations-on-uml-class-diagrams.md) [Properties of associations on UML class diagrams](../modeling/properties-of-associations-on-uml-class-diagrams.md)
