---
title: 在类设计器中重命名并移动类和类型
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.ClassDesigner.OverrideMembersDialog
helpviewer_keywords:
- members, overriding
- overriding members
- classes [Visual Studio], refactoring
- type members, overriding
- refactoring, types
- types [Visual Studio], refactoring
- Class Designer [Visual Studio], refactoring classes
- refactoring, classes
ms.assetid: dcf07bb4-fa3b-4224-9dec-566fd924a8ce
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d99fc68f6b42b442a87ead02aba888063b1b42a1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975081"
---
# <a name="refactor-classes-and-types-in-class-designer"></a>在类设计器中重构类和类型

重构代码时，通过更改它的内部结构和它的对象的设计方式，而不是更改它的外部行为，你可以让它变得更易理解、维护以及更加高效。 在 Visual Studio 项目中重构 C#、Visual Basic 或 C++ 代码时，可以通过使用类设计器和类详细信息窗口来减少必要的工作量，并降低引入 bug 的几率。

> [!NOTE]
> 项目文件可能为只读类型，原因是这个项目受源代码管理且还未签出；它是一个引用项目；或它的文件在磁盘上被标记为只读。 当正在处理的项目处于这些状态中的某一状态时，可通过多种方式保存工作，具体取决于项目的状态。 这种情况适用于重构代码，也适用于通过其他方法（如直接编辑代码）更改的代码。

## <a name="common-tasks"></a>常见任务

|任务|支持内容|
|----------| - |
|**重构类：** 可以通过重构操作将类拆分为分部类或实现抽象基类。|-   [如何：将类拆分为分部类](how-to-split-a-class-into-partial-classes.md)|
|**使用接口：** 在类设计器中，可以在类图上将接口连接至为接口方法提供代码的类，以此来实现接口。|-   [如何：实现接口](how-to-implement-an-interface.md)|
|**重构类型、类型成员和参数：** 通过使用类设计器，可以重命名类型、重写类型成员，或将它们从一种类型移动到另一种类型。 此外还可创建可以为 null 的类型。|-   [重命名类型和类型成员](#rename-types-and-type-members)<br />-   [将类型成员从一个类型移到另一个类型](#move-type-members-from-one-type-to-another)<br />-   [如何：创建可以为 null 的类型](how-to-create-a-nullable-type.md)|

## <a name="rename-types-and-type-members"></a>重命名类型和类型成员

在类设计器中，可以在类图上或在“属性”窗口中重命名类型或类型的成员。 在“类详细信息”窗口中，可以更改成员名称但不能更改类型名称。 类型或类型成员的重命名将传播到所有的窗口和旧名称出现的代码位置。

### <a name="rename-in-the-class-designer"></a>在类设计器中重命名

1. 在类图上选择类型或成员，并选择名称。

     成员名称变为可编辑状态。

2. 为类型或类型成员键入新名称

### <a name="rename-in-the-class-details-window"></a>在“类详细信息”窗口中重命名

1. 如果要显示“类详细信息”窗口，右键单击类型或类型成员，然后选择“类详细信息”。

     这时将出现“类详细信息”窗口。

2. 在“名称”  列中，更改类型成员名

3. 如果要将焦点从单元格中移开，按 Enter 键或在单元格外单击即可。

    > [!NOTE]
    > 在“类详细信息”窗口中，可以更改成员名称但不能更改类型名称。

### <a name="rename-in-the-properties-window"></a>在“属性”窗口中重命名

1. 在类图或“类详细信息”窗口上，右键单击类型或成员，然后选择“属性”。

     这时会出现“属性”窗口，并显示该类型或类型成员的属性。

2. 在“名称”  属性中，更改类型或类型成员的名称。

     新名称将传播到所有的窗口和当前项目中旧名称出现的代码位置。

## <a name="move-type-members-from-one-type-to-another"></a>将类型成员从一个类型移到另一个类型

使用“类设计器”可以将类型成员从一个类型移到另一个类型。 这两个类型必须均在当前类图中可见。

1. 在设计图面上可见的一个类型中，右键单击要移到另一个类型的成员，然后选择“剪切”。

2. 右键单击目标类型，然后选择“粘贴”。

     属性将从源类型中被移除，并出现在目标类型中。

## <a name="see-also"></a>请参阅

- [设计类和类型](designing-and-viewing-classes-and-types.md)