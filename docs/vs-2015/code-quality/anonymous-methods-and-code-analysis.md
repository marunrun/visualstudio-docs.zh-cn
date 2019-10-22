---
title: 匿名方法和代码分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- methods, anonymous
- code analysis, anonymous methods
- anonymous methods, code analysis
ms.assetid: bf0a1a9b-b954-4d46-9c0b-cee65330ad00
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 49da7d5e7f6a7731a708accb3d52fb6383ff1017
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652227"
---
# <a name="anonymous-methods-and-code-analysis"></a>匿名方法和代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*匿名方法*是没有名称的方法。 匿名方法经常用于将代码块作为委托参数进行传递。

 本主题说明代码分析如何处理与匿名方法关联的警告和指标。

## <a name="anonymous-methods-declared-in-a-member"></a>成员中声明的匿名方法
 在成员中声明的匿名方法（如方法或访问器）的警告和度量值与声明该方法的成员相关联。 它们不与调用方法的成员相关联。

 例如，在下面的类中，应针对**Method1**而不是**Method2**引发在**anonymousMethod**的声明中找到的任何警告。

```vb

      Delegate Function ADelegate(ByVal value As Integer) As Boolean
Class AClass

    Sub Method1()
        Dim anonymousMethod As ADelegate = Function(ByVal value As Integer) value > 5
        Method2(anonymousMethod)
    End SubSub Method2(ByVal anonymousMethod As ADelegate)
        anonymousMethod(10)
    End SubEnd Class
```

```csharp

      delegate void Delegate();
class Class
{
    void Method1()
    {
        Delegate anonymousMethod = delegate()
        {
          Console.WriteLine("");
        }
        Method2(anonymousMethod);
    }

    void Method2(Delegate anonymousMethod)
    {
        anonymousMethod();
    }
}
```

## <a name="inline-anonymous-methods"></a>内联匿名方法
 声明为字段的内联赋值的匿名方法的警告和度量值与构造函数相关联。 如果将字段声明为 `static` （`Shared` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]），则警告和度量值将与类构造函数相关联;否则，它们与实例构造函数相关联。

 例如，在下面的类中，将针对隐式生成的**类**的默认构造函数引发在**anonymousMethod1**的声明中找到的任何警告。 相反，在**anonymousMethod2**中找到的将应用于隐式生成的类构造函数。

```vb

  Delegate Function ADelegate(ByVal value As Integer) As BooleanClass AClass
Dim anonymousMethod1 As ADelegate = Function(ByVal value As    Integer) value > 5
Shared anonymousMethod2 As ADelegate = Function(ByVal value As     Integer) value > 5

Sub Method1()
    anonymousMethod1(10)
    anonymousMethod2(10)
End SubEnd Class
```

```csharp

      delegate void Delegate();
class Class
{
    Delegate anonymousMethod1 = delegate()
    {
       Console.WriteLine("");
    }

    static Delegate anonymousMethod2 = delegate()
    {
       Console.WriteLine("");
    }

    void Method()
    {
       anonymousMethod1();
       anonymousMethod2();
    }
}
```

 类可以包含向具有多个构造函数的字段分配值的内联匿名方法。 在这种情况下，警告和指标与所有构造函数相关联，除非该构造函数链接到同一个类中的另一个构造函数。

 例如，在下面的类中，应针对**类（int）** 和**类（字符串）** （而不是针对**类（）** ）引发在**anonymousMethod**的声明中找到的任何警告。

```vb

  Delegate Function ADelegate(ByVal value As Integer) As BooleanClass AClass

Dim anonymousMethod As ADelegate = Function(ByVal value As Integer)
value > 5

SubNew()
    New(CStr(Nothing))
End SubSub New(ByVal a As Integer)
End SubSub New(ByVal a As String)
End SubEnd Class
```

```csharp

      delegate void Delegate();
class Class
{
    Delegate anonymousMethod = delegate()
    {
       Console.WriteLine("");
    }

    Class() : this((string)null)
    {
    }

    Class(int a)
    {
    }

    Class(string a)
    {
    }
}
```

 尽管这可能看起来不到预料，但发生这种情况是因为编译器会为每个未链接到另一个构造函数的构造函数输出一个唯一方法。 由于此行为，必须单独取消**anonymousMethod**中发生的任何冲突。 这也意味着，如果引入了新的构造函数，则还必须针对新构造函数禁止显示先前针对**类（int）** 和**类（字符串）** 取消的警告。

 可以通过以下两种方式之一解决此问题。 可以在所有构造函数链的公共构造函数中声明**anonymousMethod** 。 也可以在由所有构造函数调用的初始化方法中声明它。

## <a name="see-also"></a>请参阅
 [分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)
