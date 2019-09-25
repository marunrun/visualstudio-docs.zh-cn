---
title: CA1815:重写值类型上的 Equals 和相等运算符
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1815
- OverrideEqualsAndOperatorEqualsOnValueTypes
helpviewer_keywords:
- OverrideEqualsAndOperatorEqualsOnValueTypes
- CA1815
ms.assetid: 0a8ab3a3-ee8e-46f7-985d-dcf00c89363b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 413119f7cdf473f3038ae212ac812d1987641bb1
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233544"
---
# <a name="ca1815-override-equals-and-operator-equals-on-value-types"></a>CA1815:重写值类型上的 Equals 和相等运算符

|||
|-|-|
|TypeName|OverrideEqualsAndOperatorEqualsOnValueTypes|
|CheckId|CA1815|
|类别|Microsoft.Performance|
|重大更改|不间断|

## <a name="cause"></a>原因

值类型不会重写<xref:System.Object.Equals%2A?displayProperty=fullName>或不实现相等运算符（= =）。 此规则不检查枚举。

默认情况下，此规则仅查看外部可见类型，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

对于值类型，的继承实现<xref:System.Object.Equals%2A>使用反射库，并比较所有字段的内容。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果希望用户对实例进行比较或排序，或将其用作哈希表键，则值类型应<xref:System.Object.Equals%2A>实现。 如果编程语言支持运算符重载，则还应提供相等和不等运算符的实现。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请提供的<xref:System.Object.Equals%2A>实现。 如果可以，请实现相等运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果不将值类型的实例彼此进行比较，则可以安全地禁止显示此规则发出的警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1815.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（性能）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的代码显示违反此规则的结构（值类型）：

[!code-csharp[FxCop.Performance.OverrideEqualsViolation#1](../code-quality/codesnippet/CSharp/ca1815-override-equals-and-operator-equals-on-value-types_1.cs)]

下面的代码通过重写<xref:System.ValueType.Equals%2A?displayProperty=fullName>和实现相等运算符（= =，！ =）来修复以前的冲突：

[!code-csharp[FxCop.Performance.OverrideEqualsFixed#1](../code-quality/codesnippet/CSharp/ca1815-override-equals-and-operator-equals-on-value-types_2.cs)]

## <a name="related-rules"></a>相关规则

- [CA2224重载运算符等于时重写 equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)
- [CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
- [CA2226运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

## <a name="see-also"></a>请参阅

- <xref:System.Object.Equals%2A?displayProperty=fullName>