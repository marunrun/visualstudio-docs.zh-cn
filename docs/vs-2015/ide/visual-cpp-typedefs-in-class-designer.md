---
title: 类设计器中的 Visual C++ Typedef | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.typedef
- vs.classdesigner.aliasofline
helpviewer_keywords:
- Class Designer [Visual Studio], typedefs
ms.assetid: c1984108-71fc-4d3a-b4d4-3eac2c6b4ebf
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 980c49aafba55e29714d786e492f7bb37a8ca621
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72646751"
---
# <a name="visual-c-typedefs-in-class-designer"></a>类设计器中的 Visual C++ Typedef
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Typedef 语句可在某个名称和其基础类型之间创建一个或多个间接层。 类设计器支持使用关键字 `typedef` 声明的 C++ typedef 类型，例如：

```
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
} COORD;
```

 然后你可以使用此类型来声明实例：

 `COORD OriginPoint;`

 虽然可以声明没有名称的 typedef，但类设计器不会使用你指定的标记名称，而是使用类视图生成的名称。 例如，以下声明有效，但它在类视图和类设计器中显示为名为 **__unnamed** 的对象：

```
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
};
```

 有关使用 `typedef` 类型的详细信息，请参阅 [(NOTINBUILD)typedef 说明符](https://msdn.microsoft.com/cc96cf26-ba93-4179-951e-695d1f5fdcf1)。

 C++ typedef 形状具有 typedef 中所指定类型的形状。 例如，如果源声明 `typedef class`，则形状具有圆角和标签 **Class**。 对于 `typedef struct`，形状具有方角和标签 **Struct**。

 类和结构可在其自身内声明嵌套的 typedef；因此，类和结构的形状可以将嵌套的 typedef 声明显示为嵌套形状。

 Typedef 形状支持上下文菜单中的“显示为关联”**** 和“显示为集合关联”**** 命令。

 下面列举了类设计器支持的部分 typdef 类型：

 `typedef type name`

 *name* : *type*

 typedef

 如有可能，绘制一条连接到类型 *name* 的关联行。

 `typedef void (*func)(int)`

 `func: void (*)(int)`

 typedef

 用于函数指针的 Typedef。 不绘制关联行。

 如果 typedef 的源类型为函数指针，则类设计器不显示该 typedef。

```
typedef int MyInt;
class A {
   MyInt I;
};
```

 `MyInt: int`

 typedef

 `A`

 类

 绘制一条从源类型形状指向目标类型形状的关联行。

 `Class B {};`

 `typedef B MyB;`

 `B`

 类

 `MyB : B`

 typedef

 右键单击某个 typedef 形状，然后单击“显示为关联”****，将显示该 typedef 或类以及联接这两个形状的线（类似于关联行）的**别名**。

 `typedef B MyB;`

 `typedef MyB A;`

 `MyBar : Bar`

 typedef

 同上。

```
Class B {};
typedef B MyB;

class A {
   MyB B;
};
```

 `B`

 类

 `MyB : B`

 typedef

 `A`

 类

 `MyB` 是嵌套的 typedef 形状。

 `#include <vector>`

 `...`

 `using namespace std;`

 `...`

 `typedef vector<int> MyIntVect;`

 `vector<T>`类

 `MyIntVect : vector<int>`

 typedef

 `class B {};`

 `typedef B MyB;`

 `class A : MyB {};`

 `MyB : B`

 typedef

 -> B

 `B`

 `A`

 类

 -> MyB

 类设计器不支持使用上下文菜单命令显示这种关系。

 `#include <vector>`

 `Typedef MyIntVect std::vector<int>;`

 `Class MyVect : MyIntVect {};`

 `std::vector<T>`

 类

 `MyIntVect : std::vector<int>`

 typedef

 `MyVect`

 类

 -> MyIntVect

## <a name="see-also"></a>另请参阅
 使用[Visual C++ 代码 (类设计器) ](../ide/working-with-visual-cpp-code-class-designer.md) [ (NOTINBUILD) typedef 说明符](https://msdn.microsoft.com/cc96cf26-ba93-4179-951e-695d1f5fdcf1)
