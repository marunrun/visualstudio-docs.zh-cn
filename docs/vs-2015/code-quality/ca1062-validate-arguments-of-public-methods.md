---
title: CA1062:验证公共方法的参数 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 13ea687ea9ca68693af7e2aa5c22881a36207d2e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200434"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062:验证公共方法的参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|类别|Microsoft.Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 外部可见方法取消引用一个引用参数而不验证该参数是否`null`(`Nothing`在 Visual Basic 中)。

## <a name="rule-description"></a>规则说明
 应根据检查传递给外部可见方法的所有引用参数`null`。 如果适用，引发<xref:System.ArgumentNullException>时，参数是`null`。

 如果可以从未知的程序集调用的方法，因为它被声明为公共或受保护，则应验证所有参数的方法。 如果该方法旨在只能由已知程序集调用，应使该方法内部，并应用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性为包含该方法的程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请验证每个引用参数是否为`null`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 是否确实已通过在函数中的另一个方法调用验证的取消引用的参数，可以禁止显示此规则的警告。

## <a name="example"></a>示例
 下面的示例演示与规则冲突的方法和满足该规则的方法。

 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#1)]
 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#1)]
 [!code-vb[FxCop.Design.ValidateArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#1)]

## <a name="example"></a>示例
 在[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]，此规则不会检测参数传递到另一种方法进行验证。

 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#2)]
 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#2)]
 [!code-vb[FxCop.Design.ValidateArguments#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#2)]

## <a name="example"></a>示例
 填充字段或所引用对象的属性的复制构造函数还可以违反 CA1062 规则。 复制到复制构造函数传递的对象可能是因为发生了冲突`null`(`Nothing`在 Visual Basic 中)。 若要解决冲突，请使用静态 (在 Visual Basic 中的为 Shared) 方法来检查复制的对象不为 null。

 在下面的示例`Person`类的示例中，`other`对象传递给`Person`复制构造函数可能是`null`。

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
 在下面进行了修订`Person`示例中，`other`对象传递给复制构造函数将首先检查中的 null`PassThroughNonNull`方法。

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
