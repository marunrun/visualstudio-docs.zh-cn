---
title: CA1815：重写值类型的 equals 和运算符 equals |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1815
- OverrideEqualsAndOperatorEqualsOnValueTypes
helpviewer_keywords:
- OverrideEqualsAndOperatorEqualsOnValueTypes
- CA1815
ms.assetid: 0a8ab3a3-ee8e-46f7-985d-dcf00c89363b
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fc5dc311fd85af2b6a0eb3e29e9932614ca55193
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543905"
---
# <a name="ca1815-override-equals-and-operator-equals-on-value-types"></a>CA1815:重写值类型上的 Equals 和相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|OverrideEqualsAndOperatorEqualsOnValueTypes|
|CheckId|CA1815|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 公共值类型不重写 <xref:System.Object.Equals%2A?displayProperty=fullName> ，或不实现相等运算符（= =）。 此规则不检查枚举。

## <a name="rule-description"></a>规则描述
 对于值类型，的继承实现 <xref:System.Object.Equals%2A> 使用反射库，并比较所有字段的内容。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果希望用户对实例进行比较或排序，或将其用作哈希表键，则值类型应实现 <xref:System.Object.Equals%2A> 。 如果编程语言支持运算符重载，则还应提供相等和不等运算符的实现。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请提供的实现 <xref:System.Object.Equals%2A> 。 如果可以，请实现相等运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果不将值类型的实例彼此进行比较，则可以安全地禁止显示此规则发出的警告。

## <a name="example-of-a-violation"></a>冲突示例

### <a name="description"></a>描述
 下面的示例演示违反此规则的结构（值类型）。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.OverrideEqualsViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.OverrideEqualsViolation/cs/FxCop.Performance.OverrideEqualsViolation.cs#1)]

## <a name="example-of-how-to-fix"></a>解决方法的示例

### <a name="description"></a>描述
 下面的示例通过重写 <xref:System.ValueType.Equals%2A?displayProperty=fullName> 和实现相等运算符（= =，！ =）来修复前面的冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.OverrideEqualsFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.OverrideEqualsFixed/cs/FxCop.Performance.OverrideEqualsFixed.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA2224:重载相等运算符时重写 Equals 方法](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2231:重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)

 [CA2226:运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Object.Equals%2A?displayProperty=fullName>
