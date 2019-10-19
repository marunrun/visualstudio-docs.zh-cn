---
title: CA2224：重载运算符等于时重写 equals |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2224
- OverrideEqualsOnOverloadingOperatorEquals
- OverrideEqualsOnOverridingOperatorEquals
helpviewer_keywords:
- OverrideEqualsOnOverloadingOperatorEquals
- CA2224
ms.assetid: 7312afd9-84ba-417f-923e-7a159b53bf70
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d35052bb2a1efb1a466ffc67c95c83e5b3a76533
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671881"
---
# <a name="ca2224-override-equals-on-overloading-operator-equals"></a>CA2224：重载相等运算符时重写 Equals 方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverrideEqualsOnOverloadingOperatorEquals|
|CheckId|CA2224|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 公共类型实现相等运算符，但不会重写 <xref:System.Object.Equals%2A?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 相等运算符旨在以语法上方便的方式访问 <xref:System.Object.Equals%2A> 方法的功能。 如果实现相等运算符，则其逻辑必须与 <xref:System.Object.Equals%2A> 的逻辑相同。

 如果C#代码违反此规则，编译器会发出警告。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，应删除相等运算符的实现，或重写 <xref:System.Object.Equals%2A>，并使两个方法返回相同的值。 如果相等运算符未引入不一致的行为，则可以通过提供调用基类中的 <xref:System.Object.Equals%2A> 方法的 <xref:System.Object.Equals%2A> 的实现来解决此冲突。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果相等运算符与 <xref:System.Object.Equals%2A> 的继承实现返回相同的值，则可以安全地禁止显示此规则发出的警告。 "示例" 部分包括一个可以安全地禁止显示此规则发出的警告的类型。

## <a name="examples-of-inconsistent-equality-definitions"></a>不一致的相等性定义的示例

### <a name="description"></a>描述
 下面的示例演示一个具有不一致的相等定义的类型。 `BadPoint` 通过提供相等运算符的自定义实现来更改相等性的含义，但不会重写 <xref:System.Object.Equals%2A>，使其行为完全相同。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperatorEqualsRequiresEquals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperatorEqualsRequiresEquals/cs/FxCop.Usage.OperatorEqualsRequiresEquals.cs#1)]

## <a name="example"></a>示例
 下面的代码测试 `BadPoint` 的行为。

 [!code-csharp[FxCop.Usage.TestOperatorEqualsRequiresEquals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.TestOperatorEqualsRequiresEquals/cs/FxCop.Usage.TestOperatorEqualsRequiresEquals.cs#1)]

 本示例生成以下输出。

 **a = （[0] 1，1）和 b = （[1] 2，2）相等？No** 
**a = = b？不**
**a1 和 a 是否相同？是**
**a1 = = a？是**
**b，bcopy 相等吗？No** 
**b = = bcopy？是**
## <a name="example"></a>示例
 下面的示例演示了在技术上违反此规则，但行为不一致的类型。

 [!code-csharp[FxCop.Usage.ValueTypeEquals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ValueTypeEquals/cs/FxCop.Usage.ValueTypeEquals.cs#1)]

## <a name="example"></a>示例
 下面的代码测试 `GoodPoint` 的行为。

 [!code-csharp[FxCop.Usage.TestValueTypeEquals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.TestValueTypeEquals/cs/FxCop.Usage.TestValueTypeEquals.cs#1)]

 本示例生成以下输出。

 **a = （1，1）和 b = （2，2）相等？No** 
**a = = b？不**
**a1 和 a 是否相同？是**
**a1 = = a？是**
**b，bcopy 相等吗？是**
**b = = bcopy？是**
## <a name="class-example"></a>类示例

### <a name="description"></a>描述
 下面的示例演示违反此规则的类（引用类型）。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OverrideEqualsClassViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OverrideEqualsClassViolation/cs/FxCop.Usage.OverrideEqualsClassViolation.cs#1)]

## <a name="example"></a>示例
 下面的示例通过重写 <xref:System.Object.Equals%2A?displayProperty=fullName> 来修复冲突。

 [!code-csharp[FxCop.Usage.OverrideEqualsClassFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OverrideEqualsClassFixed/cs/FxCop.Usage.OverrideEqualsClassFixed.cs#1)]

## <a name="structure-example"></a>结构示例

### <a name="description"></a>描述
 下面的示例演示违反此规则的结构（值类型）。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OverrideEqualsStructViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OverrideEqualsStructViolation/cs/FxCop.Usage.OverrideEqualsStructViolation.cs#1)]

## <a name="example"></a>示例
 下面的示例通过重写 <xref:System.ValueType.Equals%2A?displayProperty=fullName> 来修复冲突。

 [!code-csharp[FxCop.Usage.OverrideEqualsStructFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OverrideEqualsStructFixed/cs/FxCop.Usage.OverrideEqualsStructFixed.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1046：不要对引用类型重载相等运算符](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225：运算符重载具有命名的备用项](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2226：运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2218：重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
