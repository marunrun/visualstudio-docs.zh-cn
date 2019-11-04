---
title: CA1800:不要强制转换 |Microsoft Docs
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
ms.openlocfilehash: 466309cef8905faa9b659e2d3652975d815767fb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663109"
---
# <a name="ca1800-do-not-cast-unnecessarily"></a>CA1800:避免进行不必要的强制转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotCastUnnecessarily|
|CheckId|CA1800|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法对其一个参数或局部变量执行重复强制转换。 对于此规则的完整分析，必须使用调试信息生成经过测试的程序集，并且关联的程序数据库（.pdb）文件必须可用。

## <a name="rule-description"></a>规则说明
 重复强制转换会降低性能，特别是在精简的迭代语句中执行强制转换时。 对于显式重复强制转换操作，将强制转换的结果存储在局部变量中，并使用局部变量而不是重复的强制转换运算。

 如果C# `is` 运算符用于测试强制转换将在执行实际强制转换之前是否成功，请考虑改为测试 `as` 运算符的结果。 它提供的功能与 `is` 运算符执行的隐式强制转换运算相同。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请修改方法实现以最大程度地减少强制转换操作的次数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果性能不是问题，则可以安全地禁止显示此规则发出的警告，或完全忽略规则。

## <a name="example"></a>示例
 下面的示例演示一个方法，该方法通过使用C# `is` 运算符来违反规则。 第二种方法通过将 `is` 运算符替换为 `as` 运算符结果的测试来满足规则，这会将每个迭代的强制转换操作数从两个减少到一。

 [!code-csharp[FxCop.Performance.UnnecessaryCastsAsIs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCastsAsIs/cs/FxCop.Performance.UnnecessaryCastsAsIs.cs#1)]

## <a name="example"></a>示例
 下面的示例演示了一个方法 `start_Click`，该方法具有多个重复的显式转换，这违反了规则，以及一个方法 `reset_Click`，该方法通过在本地变量中存储强制转换来满足规则。

 [!code-csharp[FxCop.Performance.UnnecessaryCasts#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/cs/FxCop.Performance.UnnecessaryCasts.cs#1)]
 [!code-vb[FxCop.Performance.UnnecessaryCasts#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/vb/FxCop.Performance.UnnecessaryCasts.vb#1)]

## <a name="see-also"></a>请参阅
 [原](https://msdn.microsoft.com/library/a9be126b-cbf4-4990-a70d-d0e1983cad0e)[样](https://msdn.microsoft.com/library/bc62316a-d41f-4f90-8300-c6f4f0556e43)
