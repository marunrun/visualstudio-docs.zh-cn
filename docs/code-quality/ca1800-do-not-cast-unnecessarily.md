---
title: CA1800:避免进行不必要的强制转换
ms.date: 10/26/2017
ms.topic: reference
f1_keywords:
- CA1800
- DoNotCastUnnecessarily
helpviewer_keywords:
- DoNotCastUnnecessarily
- CA1800
ms.assetid: b79a010a-6627-421e-8955-6007e32fa808
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- VB
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 85d168e97f422a3965096a334cb2a448406604f9
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233844"
---
# <a name="ca1800-do-not-cast-unnecessarily"></a>CA1800:避免进行不必要的强制转换

|||
|-|-|
|TypeName|DoNotCastUnnecessarily|
|CheckId|CA1800|
|类别|Microsoft.Performance|
|重大更改|不间断|

## <a name="cause"></a>原因
方法对其一个参数或局部变量执行重复强制转换。

对于此规则的完整分析，必须使用调试信息生成经过测试的程序集，并且关联的程序数据库（.pdb）文件必须可用。

## <a name="rule-description"></a>规则说明
重复强制转换会降低性能，特别是在精简的迭代语句中执行强制转换时。 对于显式重复强制转换操作，将强制转换的结果存储在局部变量中，并使用局部变量而不是重复的强制转换运算。

C# `as`如果使用运算符来测试强制转换将在执行实际强制转换之前是否成功，请考虑改为测试运算符的`is`结果。 这提供了相同的功能，而无需由`is`运算符执行的隐式强制转换运算。 或者，在C# 7.0 和更高版本中`is` ，将运算符与[模式匹配](/dotnet/csharp/language-reference/keywords/is#pattern-matching-with-is)一起使用以检查类型转换，并在一个步骤中将表达式强制转换为该类型的变量。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请修改方法实现以最大程度地减少强制转换操作的次数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果性能不是问题，则可以安全地禁止显示此规则发出的警告，或完全忽略规则。

## <a name="examples"></a>示例
下面的示例演示了一个方法，该方法通过使用C# `is`运算符来违反规则。 第二个方法通过将`is`运算符替换为对`as`运算符结果进行的测试来满足规则，这会将每个迭代的强制转换操作数从两个减少到一个。 第三种方法还通过使用`is` [模式匹配](/dotnet/csharp/language-reference/keywords/is#pattern-matching-with-is)来满足规则，以便在类型转换成功的情况创建所需类型的变量。

[!code-csharp[FxCop.Performance.UnnecessaryCastsAsIs#1](../code-quality/codesnippet/CSharp/ca1800-do-not-cast-unnecessarily_1.cs)]

下面的示例演示了一个方法`start_Click`，该方法具有多个重复的显式强制转换，这违反了规则， `reset_Click`以及一个方法，该方法通过在本地变量中存储强制转换来满足规则。

[!code-vb[FxCop.Performance.UnnecessaryCasts#1](../code-quality/codesnippet/VisualBasic/ca1800-do-not-cast-unnecessarily_2.vb)]
[!code-csharp[FxCop.Performance.UnnecessaryCasts#1](../code-quality/codesnippet/CSharp/ca1800-do-not-cast-unnecessarily_2.cs)]

## <a name="see-also"></a>请参阅

- [as （C#引用）](/dotnet/csharp/language-reference/keywords/as)
- [为（C#引用）](/dotnet/csharp/language-reference/keywords/is)