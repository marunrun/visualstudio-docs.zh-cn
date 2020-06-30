---
title: CA1800：不必要地强制转换 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1800
- DoNotCastUnnecessarily
helpviewer_keywords:
- DoNotCastUnnecessarily
- CA1800
ms.assetid: b79a010a-6627-421e-8955-6007e32fa808
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 757d66ef719b3a1f39a9164dfd50ce1fcf8799db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547792"
---
# <a name="ca1800-do-not-cast-unnecessarily"></a>CA1800:避免进行不必要的强制转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotCastUnnecessarily|
|CheckId|CA1800|
|Category|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法对其一个参数或局部变量执行重复强制转换。 对于此规则的完整分析，必须使用调试信息生成经过测试的程序集，并且关联的程序数据库（.pdb）文件必须可用。

## <a name="rule-description"></a>规则描述
 重复强制转换会降低性能，特别是在精简的迭代语句中执行强制转换时。 对于显式重复强制转换操作，将强制转换的结果存储在局部变量中，并使用局部变量而不是重复的强制转换运算。

 如果使用 c # `is` 运算符来测试强制转换将在执行实际强制转换之前是否成功，请考虑改为测试运算符的结果 `as` 。 这提供了相同的功能，而无需由运算符执行的隐式强制转换运算 `is` 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请修改方法实现以最大程度地减少强制转换操作的次数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果性能不是问题，则可以安全地禁止显示此规则发出的警告，或完全忽略规则。

## <a name="example"></a>示例
 下面的示例演示了一个使用 c # 运算符来违反规则的方法 `is` 。 第二个方法通过将运算符替换为 `is` 对运算符结果进行的测试来满足规则 `as` ，这会将每个迭代的强制转换操作数从两个减少到一个。

 [!code-csharp[FxCop.Performance.UnnecessaryCastsAsIs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCastsAsIs/cs/FxCop.Performance.UnnecessaryCastsAsIs.cs#1)]

## <a name="example"></a>示例
 下面的示例演示了一个方法， `start_Click` 该方法具有多个重复的显式强制转换，这违反了规则，以及一个方法， `reset_Click` 该方法通过在本地变量中存储强制转换来满足规则。

 [!code-csharp[FxCop.Performance.UnnecessaryCasts#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/cs/FxCop.Performance.UnnecessaryCasts.cs#1)]
 [!code-vb[FxCop.Performance.UnnecessaryCasts#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/vb/FxCop.Performance.UnnecessaryCasts.vb#1)]

## <a name="see-also"></a>另请参阅
 [原样](https://msdn.microsoft.com/library/a9be126b-cbf4-4990-a70d-d0e1983cad0e) [is](https://msdn.microsoft.com/library/bc62316a-d41f-4f90-8300-c6f4f0556e43)
