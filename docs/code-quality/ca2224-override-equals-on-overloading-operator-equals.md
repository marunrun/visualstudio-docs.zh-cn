---
title: CA2224:重载相等运算符时重写 Equals 方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2224
- OverrideEqualsOnOverloadingOperatorEquals
- OverrideEqualsOnOverridingOperatorEquals
helpviewer_keywords:
- OverrideEqualsOnOverloadingOperatorEquals
- CA2224
ms.assetid: 7312afd9-84ba-417f-923e-7a159b53bf70
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3fa6bfa5b590d330d791eb8c735099e619ffaf3a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62541905"
---
# <a name="ca2224-override-equals-on-overloading-operator-equals"></a>CA2224:重载相等运算符时重写 Equals 方法

|||
|-|-|
|TypeName|OverrideEqualsOnOverloadingOperatorEquals|
|CheckId|CA2224|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

公共类型实现相等运算符，但不重写<xref:System.Object.Equals%2A?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明

相等运算符用于在语法上方便地访问的功能<xref:System.Object.Equals%2A>方法。 如果实现相等运算符时，其逻辑必须是相同的<xref:System.Object.Equals%2A>。

如果你的代码与此规则冲突，C# 编译器会发出警告。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，应删除的相等运算符的实现，或重写<xref:System.Object.Equals%2A>和具有两个方法返回相同的值。 如果相等运算符不会引入不一致的行为，则可以通过提供的实现来解决冲突<xref:System.Object.Equals%2A>的调用<xref:System.Object.Equals%2A>基类中的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

则可以安全地禁止显示此规则的警告，如果相等运算符将返回相同的值的继承的实现<xref:System.Object.Equals%2A>。 这篇文章中的示例包括一个类型，可以安全地禁止显示此规则的警告。

## <a name="examples-of-inconsistent-equality-definitions"></a>不一致的相等性定义的示例

下面的示例演示具有定义的相等性不一致的类型。 `BadPoint` 通过提供相等运算符的自定义实现更改是否相等的含义，但不会重写<xref:System.Object.Equals%2A>，以便它的行为相同。

[!code-csharp[FxCop.Usage.OperatorEqualsRequiresEquals#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_1.cs)]

下面的代码测试的行为`BadPoint`。

[!code-csharp[FxCop.Usage.TestOperatorEqualsRequiresEquals#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_2.cs)]

该示例产生下面的输出：

```txt
a =  ([0] 1,1) and b = ([1] 2,2) are equal? No
a == b ? No
a1 and a are equal? Yes
a1 == a ? Yes
b and bcopy are equal ? No
b == bcopy ? Yes
```

下面的示例演示从技术上讲违反此规则，但不会发生意外行为不一致的方式的类型。

[!code-csharp[FxCop.Usage.ValueTypeEquals#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_3.cs)]

下面的代码测试的行为`GoodPoint`。

[!code-csharp[FxCop.Usage.TestValueTypeEquals#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_4.cs)]

该示例产生下面的输出：

```txt
a =  (1,1) and b = (2,2) are equal? No
a == b ? No
a1 and a are equal? Yes
a1 == a ? Yes
b and bcopy are equal ? Yes
b == bcopy ? Yes
```

## <a name="class-example"></a>类示例

下面的示例演示与此规则冲突的类 （引用类型）。

[!code-csharp[FxCop.Usage.OverrideEqualsClassViolation#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_5.cs)]

下面的示例通过重写修复了冲突<xref:System.Object.Equals%2A?displayProperty=fullName>。

[!code-csharp[FxCop.Usage.OverrideEqualsClassFixed#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_6.cs)]

## <a name="structure-example"></a>结构示例

下面的示例显示了与此规则冲突的结构 （值类型）：

[!code-csharp[FxCop.Usage.OverrideEqualsStructViolation#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_7.cs)]

下面的示例通过重写修复了冲突<xref:System.ValueType.Equals%2A?displayProperty=fullName>。

[!code-csharp[FxCop.Usage.OverrideEqualsStructFixed#1](../code-quality/codesnippet/CSharp/ca2224-override-equals-on-overloading-operator-equals_8.cs)]

## <a name="related-rules"></a>相关的规则

[CA1046:请重载相等运算符对引用类型](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

[CA2225:运算符重载具有命名的备用项](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

[CA2226:运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

[CA2218:重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

[CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)