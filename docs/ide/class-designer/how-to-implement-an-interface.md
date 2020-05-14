---
title: 如何：实现接口（类设计器）
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interfaces [Visual Studio], implementing
- interfaces [Visual Studio]
ms.assetid: 81d2cf46-7f60-448c-83e3-1d16bb88ca36
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbe8db6c6bd7df5285880f7f860df5bb26db736a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590106"
---
# <a name="how-to-implement-an-interface-in-class-designer"></a>如何：在类设计器中实现接口

在类设计器中，可以在类图上将接口连接至为接口方法提供代码的类，以此来实现接口  。 类设计器可生成接口实现，并将接口与类之间的关系显示为继承关系  。 可以通过在接口与类之间绘制继承连线或从类视图拖动接口来实现接口。

> [!TIP]
> 创建接口的方法与创建其他类型的方法相同。 如果接口存在但未显示在类图上，则首先要显示接口。 有关详细信息，请参阅[如何：使用类设计器创建类型](how-to-create-types.md)和[如何：查看现有类型](how-to-view-existing-types.md)。

## <a name="to-implement-an-interface-by-drawing-an-inheritance-line"></a>通过绘制继承连线实现接口

1. 在类图上，显示接口和将实现该接口的类。

2. 从类和接口绘制一条继承连线。

     将有一个棒糖形附加在类上，还有一个带接口名称的标签，用以标识继承关系。 Visual Studio 为所有接口成员生成存根。

有关详细信息，请参阅[如何：创建类型之间的继承](how-to-create-inheritance-between-types.md)。

## <a name="to-implement-an-interface-from-the-class-view-window"></a>从“类视图”窗口实现接口

1. 在类图上，显示要实现接口的类。

2. 打开类视图，并查找该接口  。

    > [!TIP]
    > 如果类视图尚未打开，则从“视图”菜单或按 Ctrl**Shift**C 打开类视图    +  +  。

3. 在关系图上将接口节点拖到类形状。

     将有一个棒糖形附加在类上，还有一个带接口名称的标签，用以标识继承关系。 Visual Studio 为所有接口成员生成存根；至此就实现了接口。

## <a name="see-also"></a>另请参阅

- [如何：使用类设计器创建类型](how-to-create-types.md)
- [如何：查看现有类型](how-to-view-existing-types.md)
- [如何：创建类型之间的继承](how-to-create-inheritance-between-types.md)
- [重构类和类型](refactoring-classes-and-types.md)
