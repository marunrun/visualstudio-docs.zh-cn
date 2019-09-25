---
title: CA1812:避免未实例化的内部类
ms.date: 05/16/2019
ms.topic: reference
f1_keywords:
- CA1812
- AvoidUninstantiatedInternalClasses
helpviewer_keywords:
- AvoidUninstantiatedInternalClasses
- CA1812
ms.assetid: 1bb92a42-322a-44cc-98a8-8858212c1e1f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f924e9530a7ee43ec2222366141c3af6be2efc29
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233602"
---
# <a name="ca1812-avoid-uninstantiated-internal-classes"></a>CA1812:避免未实例化的内部类

|||
|-|-|
|TypeName|AvoidUninstantiatedInternalClasses|
|CheckId|CA1812|
|类别|Microsoft.Performance|
|重大更改|不间断|

## <a name="cause"></a>原因

内部（程序集级别）类型永远不会实例化。

## <a name="rule-description"></a>规则说明

此规则尝试查找对类型的其中一个构造函数的调用，并在找不到调用时报告冲突。

此规则不检查以下类型：

- 值类型

- 抽象类型

- 枚举

- 委托

- 编译器发出的数组类型

- 不能实例化且仅定义[`static`](/dotnet/csharp/language-reference/keywords/static) （[ `Shared`在 Visual Basic 中](/dotnet/visual-basic/language-reference/modifiers/shared)）方法的类型。

如果将应用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute?displayProperty=fullName>到正在分析的程序集，则此规则将不标记标记为[`internal`](/dotnet/csharp/language-reference/keywords/internal)的类型（[ `Friend`在 Visual Basic 中](/dotnet/visual-basic/language-reference/modifiers/friend)），因为友元程序集可能会使用某个字段。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除该类型或添加使用它的代码。 如果类型仅`static`包含方法，请将以下内容之一添加到类型中，以防止编译器发出默认的公共实例构造函数：

- 面向 .NET Framework 2.0 C#或更高版本的类型的修饰符。`static`

- 面向 .NET Framework 版本1.0 和1.1 的类型的私有构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

可以安全地禁止显示此规则发出的警告。 建议在以下情况下禁止显示此警告：

- 类是通过后期绑定反射方法（如） <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>创建的。

- 类由运行时或 ASP.NET 自动创建。 自动创建的类的一些示例是实现<xref:System.Configuration.IConfigurationSectionHandler?displayProperty=fullName>或<xref:System.Web.IHttpHandler?displayProperty=fullName>的类。

- 类作为具有[ `new`约束](/dotnet/csharp/language-reference/keywords/new-constraint)的类型参数进行传递。 下面的示例将由规则 CA1812 标记：

    ```csharp
    internal class MyClass
    {
        public DoSomething()
        {
        }
    }
    public class MyGeneric<T> where T : new()
    {
        public T Create()
        {
            return new T();
        }
    }

    MyGeneric<MyClass> mc = new MyGeneric<MyClass>();
    mc.Create();
    ```

## <a name="related-rules"></a>相关规则

- [CA1811避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)
- [CA1801查看未使用的参数](../code-quality/ca1801-review-unused-parameters.md)
- [CA1804删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)