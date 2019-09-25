---
title: CA1013:重载加法方法和减法方法时重载相等运算符
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
helpviewer_keywords:
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
ms.assetid: 5bd28d68-c179-49ff-af47-5250b8b18a10
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2bb5fd5c0e68b5dcffc212af03294d94d04d2abe
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236336"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013:重载加法方法和减法方法时重载相等运算符

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因
公共或受保护类型实现加或减运算符时没有实现相等运算符。

## <a name="rule-description"></a>规则说明
如果可以使用加法和减法等运算组合类型的实例，则几乎应始终为具有相同构成值的任意两`true`个实例定义相等性以返回。

不能在相等运算符的重载实现中使用默认的相等运算符。 这样做将导致堆栈溢出。 若要实现相等运算符，请在实现中使用对象 Equals 方法。 请参见以下示例。

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
若要修复与此规则的冲突，请实现相等运算符，使其在数学上与加法和减法运算符保持一致。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果相等运算符的默认实现为类型提供了正确的行为，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例定义了违反此`BadAddableType`规则的类型（）。 此类型应实现相等运算符，以使具有相同字段值的任意两个实例进行`true`相等性测试。 类型`GoodAddableType`显示已更正的实现。 请注意，此类型还实现不等运算符， <xref:System.Object.Equals%2A>并进行重写以满足其他规则。 还实现<xref:System.Object.GetHashCode%2A>了一个完整的实现。

[!code-csharp[FxCop.Design.AddAndSubtract#1](../code-quality/codesnippet/CSharp/ca1013-overload-operator-equals-on-overloading-add-and-subtract_1.cs)]

## <a name="example"></a>示例
下面的示例通过使用之前在本主题中定义的类型的实例来测试相等性，以说明相等运算符的默认行为和正确行为。

[!code-csharp[FxCop.Design.TestAddAndSubtract#1](../code-quality/codesnippet/CSharp/ca1013-overload-operator-equals-on-overloading-add-and-subtract_2.cs)]

该示例产生下面的输出：

```txt
Bad type:  {2,2} {2,2} are equal? No
Good type: {3,3} {3,3} are equal? Yes
Good type: {3,3} {3,3} are == ?   Yes
Bad type:  {2,2} {9,9} are equal? No
Good type: {3,3} {9,9} are == ?   No
```

## <a name="see-also"></a>请参阅

- [相等运算符](/dotnet/standard/design-guidelines/equality-operators)