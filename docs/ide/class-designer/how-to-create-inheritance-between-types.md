---
title: 如何：创建类型之间的继承（类设计器）
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.inheritanceline
helpviewer_keywords:
- inheritance, relationship defining
- relationships, defining inheritance
ms.assetid: 3786a21c-8022-4bf5-9d13-740fd354e93c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbf540056318e092db13521dc80478cc7eb91948
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590366"
---
# <a name="how-to-create-inheritance-between-types-in-class-designer"></a>如何：在类设计器中创建类型之间的继承

若要使用类设计器在类图上的两种类型之间创建继承关系，请将基类型与其派生的类型相连接  。 你可以有存在于两个类之间、类和接口之间，或者是两个接口之间的继承关系。

## <a name="to-create-an-inheritance-between-types"></a>在类型之间创建继承

1. 从解决方案资源管理器的项目中，打开一个类图 (.cd) 文件  。

     如果你尚未拥有类图，请创建一个。 请参阅[如何：向项目添加类图](how-to-add-class-diagrams-to-projects.md)。

2. 在“工具箱”的“类设计器”下，单击“继承”    。

3. 在类关系图上，在你想要的两个类型之间绘制一条继承连线，从:

    - 派生类到基类

    - 实现类到已实现接口

    - 扩展接口到已扩展接口

4. （可选）当你有从泛型类型派生的类型时，单击该继承连线。 在“属性”窗口中，设置“类型参数”属性，使其与要用于泛型类型的类型匹配   。

    > [!NOTE]
    > 如果父抽象类至少包含一个抽象成员，则所有这些成员都将作为非抽象的继承类实现。
    >
    >  尽管可对现有泛型类型进行可视化，但不能创建新的泛型类型。 还不能更改现有泛型类型的类型参数。

## <a name="see-also"></a>请参阅

- [继承](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
- [继承的基础知识](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [如何：查看类型之间的继承](how-to-view-inheritance-between-types.md)
- [类设计器中的 Visual C++ 类](visual-cpp-classes.md)
