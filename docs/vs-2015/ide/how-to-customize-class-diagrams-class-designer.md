---
title: 如何：自定义类图（类设计器）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- class diagrams, customizing
- shapes, removing type from class diagrams
- type shapes, removing from class diagrams
- class diagrams, removing type shapes
ms.assetid: e9030aea-c77d-4cc1-b8f6-b6ca469b692d
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ff78bea6759359d3703f5fed6157f051c89befb0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668012"
---
# <a name="how-to-customize-class-diagrams-class-designer"></a>如何：自定义类图（类设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以更改类图显示信息的方式。 可以在设计图面上自定义整个关系图或各个类型。

 例如，你可以调整整个类图的缩放级别，更改各个类型成员的分组和排序方式，隐藏或显示关系并将单个类型或类型集移动到类图上的任意位置。

> [!NOTE]
> 自定义类图上的形状显示方式不会更改类图上表示的类型的基础代码。

 包含类型成员的部分（例如类中的“属性”部分）被称为隔离舱。 你可以隐藏或显示各个隔离舱和类型成员。

 **主题内容**

- [放大和缩小类图](../ide/how-to-customize-class-diagrams-class-designer.md#ZoomInOut)

- [自定义类型成员的分组和排序](../ide/how-to-customize-class-diagrams-class-designer.md#CustomizeGroupingSorting)

- [隐藏类型中的隔离舱](../ide/how-to-customize-class-diagrams-class-designer.md#HideCompartments)

- [隐藏类型中的各个成员](../ide/how-to-customize-class-diagrams-class-designer.md#HideMembers)

- [显示类型中隐藏的隔离舱和成员](../ide/how-to-customize-class-diagrams-class-designer.md#DisplayHiddenCompartmentsAndMemberrs)

- [隐藏关系](../ide/how-to-customize-class-diagrams-class-designer.md#HideAssociationAndInheritance)

- [显示隐藏的关系](../ide/how-to-customize-class-diagrams-class-designer.md#DisplayAssociationAndInheritance)

- [从类图中删除形状](../ide/how-to-customize-class-diagrams-class-designer.md#RemoveCodeAndShape)

- [删除类型形状及其基础代码](../ide/how-to-customize-class-diagrams-class-designer.md#DeleteTypeShapeAndCode)

## <a name="ZoomInOut"></a> 放大和缩小类图

1. 在类设计器中打开并选择类图文件。

2. 在“类设计器”工具栏中，单击“放大”或“缩小”按钮以更改设计器图面的缩放级别。

     或

     指定特定的缩放值。 可以使用“缩放”下拉列表进行选择或键入有效的缩放级别（有效范围介于 10% 到 400% 之间）。

    > [!NOTE]
    > 更改缩放级别并不影响类图的打印输出比例。

## <a name="CustomizeGroupingSorting"></a> 自定义类型成员的分组和排序

1. 在类设计器中打开并选择类图文件。

2. 右键单击设计图面上的空白区域，然后指向“组成员”。

3. 选择下列可用选项之一：

    1. “按种类分组”将各个类型成员组织到包含“属性”、“方法”、“事件”和“字段”等组的分组列表中。 各个组依赖于实体定义：例如，如果没有为某个类定义事件，该类将不会显示任何事件组。

    2. “按访问分组”根据类型成员的访问修饰符，将各个成员组织到一个分组列表中。 例如，Public 和 Private。

    3. “按字母顺序排序”将组成实体的各个项显示为一个按字母顺序排序的列表。 此列表按升序排序。

## <a name="HideCompartments"></a> 隐藏类型中的隔离舱

1. 在类设计器中打开并选择类图文件。

2. 在要自定义的类型中右键单击成员类别（例如，在类中选择“方法”节点）。

3. 单击“隐藏隔离舱”。

     选定的隔离舱将从类型容器中消失。

## <a name="HideMembers"></a> 隐藏类型中的各个成员

1. 在类设计器中打开并选择类图文件。

2. 在类型中右击要隐藏的成员。

3. 单击“隐藏”。

     选定的成员将从类型容器中消失。

## <a name="DisplayHiddenCompartmentsAndMemberrs"></a> 显示类型中隐藏的隔离舱和成员

1. 在类设计器中打开并选择类图文件。

2. 右击具有隐藏的隔离舱的类型的名称。

3. 单击“显示所有成员”。

     所有隐藏的隔离舱和成员将显示在类型容器中。

## <a name="HideAssociationAndInheritance"></a> 隐藏关系

1. 在类设计器中打开并选择类图文件。

2. 右击要隐藏的关联连线或继承连线。

3. 对关联行单击“隐藏”，对继承行单击“隐藏继承行”。

4. 单击“显示所有成员”。

     所有隐藏的隔离舱和成员将显示在类型容器中。

## <a name="DisplayAssociationAndInheritance"></a> 显示隐藏的关系

1. 在类设计器中打开并选择类图文件。

2. 右击具有隐藏的关联或继承的类型。

   对关联行单击“显示所有成员”，对继承行单击“显示基类”或“显示派生类”。

## <a name="RemoveCodeAndShape"></a> 从类图中删除形状
 你可以在不影响类型的基础代码的情况下从类图中删除类型形状。 从类图移除类型形状只会影响该关系图：定义类型的基础代码和显示类型的其他关系图不受影响。

1. 在类图上，选择想要从关系图中移除的类型形状。

2. 在“编辑”菜单上选择“从关系图中移除”。

     该类型形状及与其相连的任何关联连线或继承连线都不再出现在关系图上。

## <a name="DeleteTypeShapeAndCode"></a> 删除类型形状及其基础代码

1. 在设计图面上右击形状。

2. 从上下文菜单中选择“删除代码”。

     此时即会从关系图中移除形状，并从项目中删除形状的基础代码。

## <a name="see-also"></a>请参阅
 [使用类图（类设计器）](../ide/working-with-class-diagrams-class-designer.md) [如何：在成员表示法与关联表示法之间切换（类设计器）](../ide/how-to-change-between-member-notation-and-association-notation-class-designer.md) [如何：查看现有类型（类设计器）](../ide/how-to-view-existing-types-class-designer.md) [查看类型和关系（类设计器）](../ide/viewing-types-and-relationships-class-designer.md)
