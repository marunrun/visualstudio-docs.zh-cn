---
title: CA2225：运算符重载具有命名的替换 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperatorOverloadsHaveNamedAlternates
- CA2225
helpviewer_keywords:
- OperatorOverloadsHaveNamedAlternates
- CA2225
ms.assetid: af8f7ab1-63ad-4861-afb9-b7a7a2be15e1
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 212abc1fa5e2debfaf7ca81d82c8d94e9ddb0879
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658878"
---
# <a name="ca2225-operator-overloads-have-named-alternates"></a>CA2225：运算符重载具有命名的备用项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OperatorOverloadsHaveNamedAlternates|
|CheckId|CA2225|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 检测到运算符重载，但未找到预期的指定备用方法。

## <a name="rule-description"></a>规则说明
 运算符重载允许使用符号来表示类型的计算。 例如，重载加号（+）以添加的类型通常具有一个名为 "Add" 的备用成员。 命名的备用成员提供与运算符相同的功能的访问权限，并且为以不支持重载运算符的语言编写的开发人员提供。

 此规则检查下表中列出的运算符。

|C#|Visual Basic|C++|备用名称|
|---------|------------------|-----------|--------------------|
|+ （二进制）|+|+ （二进制）|添加|
|+=|+=|+=|添加|
|&|And|&|BitwiseAnd|
|&=|And =|&=|BitwiseAnd|
|&#124;|Or|&#124;|BitwiseOr|
|&#124;=|Or =|&#124;=|BitwiseOr|
|--|不可用|--|递减|
|/|/|/|除|
|/=|/=|/=|除|
|==|=|==|Equals|
|^|Xor|^|Xor|
|^=|Xor =|^=|Xor|
|>|>|>|比较|
|>=|>=|>=|比较|
|++|不可用|++|递增|
|<>|!=|Equals|
|<<|<<|<<|从左向右|
|<<=|<<=|<<=|从左向右|
|<|<|<|比较|
|<=|<=|\<=|比较|
|&&|不可用|&&|LogicalAnd|
|&#124;&#124;|不可用|&#124;&#124;|LogicalOr|
|!|不可用|!|LogicalNot|
|%|Mod|%|Mod 或余数|
|%=|不可用|%=|Mod|
|* （二进制）|*|*|相乘|
|*=|不可用|*=|相乘|
|~|非|~|OnesComplement|
|>>|>>|>>|右 shift|
=|不可用|>>=|右 shift|
|-（二进制）|-（二进制）|-（二进制）|减|
|-=|不可用|-=|减|
|true|IsTrue|不可用|IsTrue （属性）|
|-（一元）|不可用|-|抵消|
|+ （一元）|不可用|+|加大|
|False|IsFalse|False|IsTrue （属性）|

 不能以所选语言重载 N/A = =。

 此规则还通过检查名为 `ToSomeType` 和 `FromSomeType` 的方法，检查类型（`SomeType`）中的隐式和显式强制转换运算符。

 在C#中，当重载二元运算符时，也会隐式重载相应的赋值运算符（如果有）。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请为运算符实现替代方法;使用建议的备用名称将其命名为。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果要实现共享库，请勿禁止显示此规则发出的警告。 应用程序可以忽略此规则发出的警告。

## <a name="example"></a>示例
 下面的示例定义了违反此规则的结构。 若要更正此示例，请将公共 `Add(int x, int y)` 方法添加到该结构中。

 [!code-csharp[FxCop.Usage.OperatorOverloadsHaveNamedAlternates#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperatorOverloadsHaveNamedAlternates/cs/FxCop.Usage.OperatorOverloadsHaveNamedAlternates.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1046：不要对引用类型重载相等运算符](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2226：运算符应有对称重载](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224：重载相等运算符时重写 Equals 方法](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218：重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
