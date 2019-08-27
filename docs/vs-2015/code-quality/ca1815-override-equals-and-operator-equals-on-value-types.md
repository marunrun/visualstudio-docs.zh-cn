---
title: CA1815:重写 equals 和相等运算符值类型上 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e21585a7a56fde2fb46ea86adde92eecfd1a4565
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201694"
---
# <a name="ca1815-override-equals-and-operator-equals-on-value-types"></a>CA1815:重写值类型上的 Equals 和相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverrideEqualsAndOperatorEqualsOnValueTypes|
|CheckId|CA1815|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共值类型不重写<xref:System.Object.Equals%2A?displayProperty=fullName>，或未实现相等运算符 （= =）。 此规则不会检查枚举。

## <a name="rule-description"></a>规则说明
 对于值类型，继承的实现<xref:System.Object.Equals%2A>使用反射库，并将所有字段的内容进行比较。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果期望用户比较或排序的实例，或将它们用作哈希表键，则值类型应实现<xref:System.Object.Equals%2A>。 如果编程语言支持运算符重载，则还应提供相等和不等运算符的实现。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请提供的实现<xref:System.Object.Equals%2A>。 如果可以实现相等运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果不相互进行比较的值类型的实例。

## <a name="example-of-a-violation"></a>冲突的示例

### <a name="description"></a>描述
 下面的示例显示了与此规则冲突的结构 （值类型）。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.OverrideEqualsViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.OverrideEqualsViolation/cs/FxCop.Performance.OverrideEqualsViolation.cs#1)]

## <a name="example-of-how-to-fix"></a>修复方法的示例

### <a name="description"></a>描述
 下面的示例通过重写修复上一冲突<xref:System.ValueType.Equals%2A?displayProperty=fullName>和实现相等运算符 (= =、 ！ =)。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.OverrideEqualsFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.OverrideEqualsFixed/cs/FxCop.Performance.OverrideEqualsFixed.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA2224:重写 equals 方法重载相等运算符](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)

 [CA2226:运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

## <a name="see-also"></a>请参阅
 <xref:System.Object.Equals%2A?displayProperty=fullName>
