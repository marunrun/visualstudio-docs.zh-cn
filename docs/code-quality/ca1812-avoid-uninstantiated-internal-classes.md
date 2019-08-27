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
ms.openlocfilehash: 6946434708e38bde7f6efcfc8404da14f91b41ee
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744704"
---
# <a name="ca1812-avoid-uninstantiated-internal-classes"></a>CA1812:避免未实例化的内部类

|||
|-|-|
|TypeName|AvoidUninstantiatedInternalClasses|
|CheckId|CA1812|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因

永远不会实例化的内部 （程序集级别） 类型。

## <a name="rule-description"></a>规则说明

此规则会尝试查找一个类型的构造函数调用，并报告冲突，如果不找到任何调用。

该规则不检查以下类型：

- 值类型

- 抽象类型

- 枚举

- 委托

- 编译器发出的数组类型

- 类型不能实例化，且仅定义了[ `static` ](/dotnet/csharp/language-reference/keywords/static) ([ `Shared` Visual Basic 中](/dotnet/visual-basic/language-reference/modifiers/shared)) 方法。

如果将应用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute?displayProperty=fullName>到要分析的程序集，此规则将标记作为标记的类型[ `internal` ](/dotnet/csharp/language-reference/keywords/internal) ([ `Friend`在 Visual Basic 中](/dotnet/visual-basic/language-reference/modifiers/friend)) 字段可能是因为由友元程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请删除类型或添加使用它的代码。 如果该类型仅包含`static`向要阻止编译器发出的默认公共实例构造函数的类型的方法，添加以下项之一：

- `static`修饰符C#.NET Framework 2.0 或更高版本为目标的类型。

- 私有构造函数的类型的目标.NET Framework 1.0 和 1.1 版。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告。 我们建议您取消显示在以下情况下的此警告：

- 如通过反射后期绑定方法创建的类<xref:System.Activator.CreateInstance%2A?displayProperty=fullName>。

- 类是由运行时或 ASP.NET 会自动创建。 自动创建类的一些示例包括实现的那些<xref:System.Configuration.IConfigurationSectionHandler?displayProperty=fullName>或<xref:System.Web.IHttpHandler?displayProperty=fullName>。

- 类作为具有一个类型参数传递[`new`约束](/dotnet/csharp/language-reference/keywords/new-constraint)。 下面的示例将由规则 CA1812 标记：

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

## <a name="related-rules"></a>相关的规则

- [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)
- [CA1801:检查未使用的参数](../code-quality/ca1801-review-unused-parameters.md)
- [CA1804:删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)