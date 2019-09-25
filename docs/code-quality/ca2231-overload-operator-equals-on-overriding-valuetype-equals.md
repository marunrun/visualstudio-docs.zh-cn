---
title: CA2231:重写 ValueType.Equals 时应重载相等运算符
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
- OverrideOperatorEqualsOnOverridingValueTypeEquals
helpviewer_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
ms.assetid: 114c0161-261a-40ad-8b2c-0932d6909d2a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: b5826633737c3bb7d8f358ff090f0b1a55ac8eef
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231047"
---
# <a name="ca2231-overload-operator-equals-on-overriding-valuetypeequals"></a>CA2231:重写 ValueType.Equals 时应重载相等运算符

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverridingValueTypeEquals|
|CheckId|CA2231|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

值类型会重<xref:System.Object.Equals%2A?displayProperty=fullName>写，但不实现相等运算符。

默认情况下，此规则仅查看外部可见类型，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

在大多数编程语言中，值类型没有对相等运算符（= =）的默认实现。 如果你的编程语言支持运算符重载，则应考虑实现相等运算符。 它的行为应与的行为相同<xref:System.Object.Equals%2A>。

不能在相等运算符的重载实现中使用默认的相等运算符。 这样做将导致堆栈溢出。 若要实现相等运算符，请在实现中使用对象 Equals 方法。 例如:

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请实现相等运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

可以安全地禁止显示此规则发出的警告;但是，我们建议您尽可能地提供相等运算符。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca2231.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（使用情况）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的示例定义了违反此规则的类型：

[!code-csharp[FxCop.Usage.EqualsGetHashCode#1](../code-quality/codesnippet/CSharp/ca2231-overload-operator-equals-on-overriding-valuetype-equals_1.cs)]

## <a name="related-rules"></a>相关规则

- [CA1046不要对引用类型重载运算符 equals](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)
- [CA2225运算符重载具有命名的备用项](../code-quality/ca2225-operator-overloads-have-named-alternates.md)
- [CA2226运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)
- [CA2224重载运算符等于时重写 equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)
- [CA2218重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

## <a name="see-also"></a>请参阅

- <xref:System.Object.Equals%2A?displayProperty=fullName>