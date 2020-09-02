---
title: 如何：创建类型之间的继承（类设计器）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.inheritanceline
helpviewer_keywords:
- inheritance, relationship defining
- relationships, defining inheritance
ms.assetid: 3786a21c-8022-4bf5-9d13-740fd354e93c
caps.latest.revision: 34
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba27b32cc322da2e14cec86b878a7dd42dae0039
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668104"
---
# <a name="how-to-create-inheritance-between-types-class-designer"></a>如何：创建类型之间的继承（类设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要使用类设计器在类图上的两种类型之间创建继承关系，请将基类型与其派生的类型相连接。 你可以有存在于两个类之间、类和接口之间，或者是两个接口之间的继承关系。

### <a name="to-create-an-inheritance-between-types"></a>在类型之间创建继承

1. 从解决方案资源管理器中的项目打开一个类图 (.cd) 文件。

     如果你尚未拥有类图，请创建一个。 请参阅[如何：向项目中添加类图（类设计器）](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)。

2. 在“工具箱”的“类设计器”下，单击“继承”************。

3. 在类关系图上，在你想要的两个类型之间绘制一条继承连线，从:

    - 派生类到基类

    - 实现类到已实现接口

    - 扩展接口到已扩展接口

4. （可选）当你有从泛型类型派生的类型时，单击该继承连线。 在“属性”窗口中，设置“类型参数”属性，使其与要用于泛型类型的类型匹配********。

    > [!NOTE]
    > 如果父抽象类至少包含一个抽象成员，则所有这些成员都将作为非抽象的继承类实现。
    >
    >  尽管可对现有泛型类型进行可视化，但不能创建新的泛型类型。 还不能更改现有泛型类型的类型参数。

## <a name="see-also"></a>另请参阅
 [继承](https://msdn.microsoft.com/library/81d64ee4-50f9-4d6c-a8dc-257c348d2eea)[继承基础知识](https://msdn.microsoft.com/library/dfc8deba-f5b3-4d1d-a937-7cb826446fc5)[如何：查看类型之间的继承 (类设计器](../ide/how-to-view-inheritance-between-types-class-designer.md)[中的) Visual C++ 类类设计器](../ide/visual-cpp-classes-in-class-designer.md)
