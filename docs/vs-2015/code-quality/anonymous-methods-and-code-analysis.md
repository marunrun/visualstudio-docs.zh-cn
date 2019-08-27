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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b8b3f64a0b5f70067367e98d7e1d1471fc670099
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157065"
---
# <a name="anonymous-methods-and-code-analysis"></a>匿名方法和代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*匿名方法*是没有名称的方法。 匿名方法最常用于将代码块作为委托参数传递。  
  
 本主题说明代码分析警告和与匿名方法相关联的度量值的处理。  
  
## <a name="anonymous-methods-declared-in-a-member"></a>在成员中声明的匿名方法  
 警告和成员，如方法或访问器中, 声明的匿名方法的指标与相关联的成员的声明的方法。 它们不会调用方法的成员与相关联。  
  
 例如，在下面的类的声明中找到的任何警告**anonymousMethod**应针对引发**Method1**而不**Method2**。  
  
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
 警告和被声明为内联的字段赋值的匿名方法的指标是与构造函数相关联。 如果该字段声明为`static`(`Shared`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)])、 警告和度量值是与类构造函数相关联; 否则为它们与实例构造函数相关联。  
  
 例如，在下面的类的声明中找到的任何警告**anonymousMethod1**针对的隐式生成的默认构造函数将引发**类**。 而这些中找到**anonymousMethod2**将适用于现用的隐式生成的类构造函数。  
  
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
  
 类可以包含的内联匿名方法的值赋给具有多个构造函数的字段。 在这种情况下，警告和度量值与相关联的所有构造函数除非该构造函数链接到同一个类中的另一个构造函数。  
  
 例如，在下面的类的声明中找到的任何警告**anonymousMethod**应针对引发**Class(int)** 并**Class(string)** 但不是针对**Class()** 。  
  
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
  
 尽管这看起来可能意外，这是因为编译器输出每个未链接到另一个构造函数的构造函数的唯一方法。 由于此行为，任何违反它将出现在**anonymousMethod**必须单独取消。 这还意味着，如果是新的构造函数中引入，已针对以前禁止显示警告**Class(int)** 并**Class(string)** 还必须取消对新的构造函数。  
  
 您可以解决此问题在两种方式之一。 您可以声明**anonymousMethod**常见构造函数中的所有构造函数链。 也可以由所有构造函数调用的初始化方法中声明它。  
  
## <a name="see-also"></a>请参阅  
 [分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)
