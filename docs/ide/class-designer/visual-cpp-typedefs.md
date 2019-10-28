---
title: 类设计器中的 C++ Typedef
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.typedef
- vs.classdesigner.aliasofline
helpviewer_keywords:
- Class Designer [Visual Studio], typedefs
ms.assetid: c1984108-71fc-4d3a-b4d4-3eac2c6b4ebf
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 94dc4a6687a2aaede7fc901884c5d3acc6fbf56f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747999"
---
# <a name="c-typedefs-in-class-designer"></a>类设计器中的 C++ Typedef

[Typedef](/cpp/cpp/aliases-and-typedefs-cpp#typedefs) 语句可在某个名称和其基础类型之间创建一个或多个间接层。 “类设计器”  支持使用关键字 `typedef` 声明的 C++ typedef 类型，例如：

```cpp
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
} COORD;
```

然后你可以使用此类型来声明实例：

`COORD OriginPoint;`

## <a name="class-and-struct-shapes"></a>类和结构形状

在“类设计器”  中，C++ typedef 具有 typedef 中所指定类型的形状。 如果源声明 `typedef class`，则形状具有圆角和标签“类”  。 对于 `typedef struct`，形状具有方角和标签 **Struct**。

类和结构可在自身内声明嵌套的 typedef。 在“类设计器”  中，类和结构形状可将嵌套的 typedef 声明显示为嵌套的形状。

Typedef 形状支持右键单击菜单（关联菜单）中的“显示为关联”  和“显示为集合关联”  命令。

### <a name="class-typedef-example"></a>类 typedef 示例

```cpp
class B {};
typedef B MyB;
```

![类设计器中的 C++ 类 typedef](media/cpp-class-typedef.png)

### <a name="struct-typedef-example"></a>结构 typedef 示例

```cpp
typedef struct mystructtag
{
    int   i;
    double f;
} mystruct;
```

![类设计器中的 C++ 结构 typedef](media/cpp-struct-typedef.png)

## <a name="unnamed-typedefs"></a>未命名的 typedef

虽然可以声明没有名称的 typedef，但“类设计器”不会使用指定的标记名称  。 “类设计器”  使用“类视图”  生成的名称。 例如，以下声明有效，但它在类视图和类设计器中显示为名为 __unnamed 的对象    ：

```cpp
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
};
```

> [!NOTE]
> “类设计器”不显示其源类型为函数指针的 typedef  。

## <a name="see-also"></a>请参阅

- [使用 C++代码](working-with-visual-cpp-code.md)
- [Typedefs](/cpp/cpp/aliases-and-typedefs-cpp#typedefs)