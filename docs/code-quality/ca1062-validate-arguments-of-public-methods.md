---
title: CA1062:验证公共方法的参数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
- Validate arguments of public methods
helpviewer_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8106a4c0244cbd79e88a2bdc50e04ea74627dab4
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235337"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062:验证公共方法的参数

|||
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因

外部可见方法取消引用其中一个引用参数，而不验证该参数是否`null`为`Nothing` （在 Visual Basic 中）。

## <a name="rule-description"></a>规则说明

应检查`null`传递给外部可见方法的所有引用参数。 如果需要，则<xref:System.ArgumentNullException>在参数为`null`时引发。

如果可从未知程序集调用方法，因为该方法被声明为公共或受保护的，则应验证该方法的所有参数。 如果该方法设计为仅由已知程序集调用，则应将该方法设置为内部方法， <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>并将该特性应用于包含该方法的程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请对`null`的每个引用参数进行验证。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果确定取消引用的参数已由函数中的其他方法调用验证，则可以禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示违反规则的方法和满足规则的方法。

```csharp
using System;

namespace DesignLibrary
{
    public class Test
    {
        // This method violates the rule.
        public void DoNotValidate(string input)
        {
            if (input.Length != 0)
            {
                Console.WriteLine(input);
            }
        }

        // This method satisfies the rule.
        public void Validate(string input)
        {
            if (input == null)
            {
                throw new ArgumentNullException("input");
            }
            if (input.Length != 0)
            {
                Console.WriteLine(input);
            }
        }
    }
}
```

```vb
Imports System

Namespace DesignLibrary

    Public Class Test

        ' This method violates the rule.
        Sub DoNotValidate(ByVal input As String)

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

        ' This method satisfies the rule.
        Sub Validate(ByVal input As String)

            If input Is Nothing Then
                Throw New ArgumentNullException("input")
            End If

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

    End Class

End Namespace
```

## <a name="example"></a>示例

填充作为引用对象的字段或属性的复制构造函数也可能违反 CA1062 规则。 发生冲突的原因是，传递到复制构造函数的复制的对象可能`null`是`Nothing` （Visual Basic）。 若要解决此冲突，请使用静态方法（在 Visual Basic 中共享）检查复制的对象是否不为 null。

在下面`Person`的类示例中`other` ，传递给`Person`复制构造函数的对象可能是`null`。

```csharp
public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor CA1062 fires because other is dereferenced
    // without being checked for null
    public Person(Person other)
        : this(other.Name, other.Age)
    {
    }
}
```

## <a name="example"></a>示例

在下面的修订`Person`示例中`other` ，首先在`PassThroughNonNull`方法中检查传递给复制构造函数的对象是否为 null。

```csharp
public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor
    public Person(Person other)
        : this(PassThroughNonNull(other).Name,
          PassThroughNonNull(other).Age)
    {
    }

    // Null check method
    private static Person PassThroughNonNull(Person person)
    {
        if (person == null)
            throw new ArgumentNullException("person");
        return person;
    }
}
```