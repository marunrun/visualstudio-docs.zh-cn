---
title: CA1062：验证公共方法的参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
- Validate arguments of public methods
helpviewer_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
ms.assetid: db1f69ca-68f7-477e-94f3-d135cc5dfcbc
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 377906675d70a712f8ca72b0b6e4d8a6864c1fbc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533232"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062:验证公共方法的参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|类别|Microsoft. Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 外部可见方法取消引用其中一个引用参数，而不验证该参数是否为 `null` （ `Nothing` 在 Visual Basic 中）。

## <a name="rule-description"></a>规则描述
 应检查传递给外部可见方法的所有引用参数 `null` 。 如果需要，则 <xref:System.ArgumentNullException> 在参数为时引发 `null` 。

 如果可从未知程序集调用方法，因为该方法被声明为公共或受保护的，则应验证该方法的所有参数。 如果该方法设计为仅由已知程序集调用，则应将该方法设置为内部方法，并将该特性应用于 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 包含该方法的程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请对的每个引用参数进行验证 `null` 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果确定取消引用的参数已由函数中的其他方法调用验证，则可以禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的方法和满足规则的方法。

 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#1)]
 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#1)]
 [!code-vb[FxCop.Design.ValidateArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#1)]

## <a name="example"></a>示例
 在中 [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] ，此规则不检测将参数传递给执行验证的另一种方法。

 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#2)]
 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#2)]
 [!code-vb[FxCop.Design.ValidateArguments#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#2)]

## <a name="example"></a>示例
 填充作为引用对象的字段或属性的复制构造函数也可能违反 CA1062 规则。 发生冲突的原因是，传递到复制构造函数的复制的对象可能是 `null` （ `Nothing` Visual Basic）。 若要解决此冲突，请使用静态方法（在 Visual Basic 中共享）检查复制的对象是否不为 null。

 在下面的 `Person` 类示例中， `other` 传递给 `Person` 复制构造函数的对象可能是 `null` 。

```

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
 在下面的修订 `Person` 示例中， `other` 首先在方法中检查传递给复制构造函数的对象是否为 null `PassThroughNonNull` 。

```
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
