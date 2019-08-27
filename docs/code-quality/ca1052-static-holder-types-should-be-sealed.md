---
title: CA1052:静态容器类型应为 Static 或 NotInheritable
ms.date: 07/25/2019
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldBeSealed
- CA1052
helpviewer_keywords:
- CA1052
- StaticHolderTypesShouldBeSealed
ms.assetid: 51a3165d-781e-4a55-aa0d-ea25fee7d4f2
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: ba54b9f87fe8c8cd8bfdc86f39e3121135241e92
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547515"
---
# <a name="ca1052-static-holder-types-should-be-static-or-notinheritable"></a>CA1052:静态容器类型应为 Static 或 NotInheritable

|||
|-|-|
|TypeName|StaticHolderTypesAnalyzer|
|CheckId|CA1052|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因

非抽象类型仅包含静态成员 (不是可能的默认构造函数), 且不使用[静态](/dotnet/csharp/language-reference/keywords/static)修饰符或[共享](/dotnet/visual-basic/language-reference/modifiers/shared)修饰符进行声明。

默认情况下, 此规则仅查看外部可见类型, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

规则 CA1052 假定只包含静态成员的类型不能被继承, 因为该类型不提供可在派生类型中重写的任何功能。 应使用中`static` C#的修饰符标记不应继承的类型, 以禁止将其用作基类型。 此外, 应移除其默认构造函数。 在 Visual Basic 中, 应将类转换为[模块](/dotnet/visual-basic/language-reference/statements/module-statement)。

对于具有基类的抽象类或类, 不会触发此规则。 但是, 对于支持空接口的类, 会激发规则。

> [!NOTE]
> 在此规则的 FxCop 分析器实现中, 它还包含[规则 CA1053](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)的功能。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突, 请将类型`static`标记为并删除默认构造C#函数 (), 或将其转换为模块 (Visual Basic)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当类型设计为继承时, 禁止显示此规则发出的警告。 缺少`static`修饰符表明类型可用作基类型。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 EditorConfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1052.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (设计) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example-of-a-violation"></a>冲突示例

下面的示例演示违反规则的类型:

[!code-csharp[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/CSharp/ca1052-static-holder-types-should-be-sealed_1.cs)]
[!code-vb[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/VisualBasic/ca1052-static-holder-types-should-be-sealed_1.vb)]
[!code-cpp[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/CPP/ca1052-static-holder-types-should-be-sealed_1.cpp)]

## <a name="fix-with-the-static-modifier"></a>用 static 修饰符修复

下面的示例演示如何通过在中`static` C#使用修饰符标记类型来修复此规则的冲突:

```csharp
public static class StaticMembers
{
    public static int SomeProperty { get; set; }
    public static void SomeMethod() { }
}
```