---
title: CA2231:重写 valuetype.equals 时重载运算符等于 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
- OverrideOperatorEqualsOnOverridingValueTypeEquals
helpviewer_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
ms.assetid: 114c0161-261a-40ad-8b2c-0932d6909d2a
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 679df7b916740ad1a45d624f9f50d38c94d64caf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201563"
---
# <a name="ca2231-overload-operator-equals-on-overriding-valuetypeequals"></a>CA2231:重写 ValueType.Equals 时应重载相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverridingValueTypeEquals|
|CheckId|CA2231|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 值类型重写<xref:System.Object.Equals%2A?displayProperty=fullName>，但没有实现相等运算符。

## <a name="rule-description"></a>规则说明
 大多数编程语言中，没有默认实现相等运算符 （= =） 的值类型。 如果您的编程语言支持运算符重载，则应考虑实现相等运算符。 其行为应该是相同的<xref:System.Object.Equals%2A>。

 相等运算符的重载实现中，不能使用默认的相等运算符。 执行此操作将导致堆栈溢出。 若要实现相等运算符，请在实现中使用 Object.Equals 方法。 例如：

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
 若要修复此规则的冲突，请实现相等运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 则可以安全地禁止显示此规则; 的警告但是，我们建议在可能的情况提供相等运算符。

## <a name="example"></a>示例
 下面的示例定义与此规则冲突的类型。

 [!code-csharp[FxCop.Usage.EqualsGetHashCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.EqualsGetHashCode/cs/FxCop.Usage.EqualsGetHashCode.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1046:请重载相等运算符对引用类型](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225:运算符重载具有命名的备用项](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2226:运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224:重写 equals 方法重载相等运算符](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218:重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

## <a name="see-also"></a>请参阅
 <xref:System.Object.Equals%2A?displayProperty=fullName>
