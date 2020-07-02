---
title: CA2242：正确测试 NaN |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TestForNaNCorrectly
- CA2242
helpviewer_keywords:
- CA2242
ms.assetid: e12dcffc-e255-4e1e-8fdf-3c6054d44abe
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0c832b7eb4a94506c5e15dfa5858bb9f6753912
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546258"
---
# <a name="ca2242-test-for-nan-correctly"></a>CA2242:正确测试 NaN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|TestForNaNCorrectly|
|CheckId|CA2242|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 表达式根据或测试值 <xref:System.Single.NaN?displayProperty=fullName> <xref:System.Double.NaN?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 <xref:System.Double.NaN?displayProperty=fullName>如果未定义算术运算，则表示不是数字的结果。 测试值是否相等并始终返回的任何表达式 <xref:System.Double.NaN?displayProperty=fullName> `false` 。 对值进行不相等测试并始终返回的任何表达式 <xref:System.Double.NaN?displayProperty=fullName> `true` 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，并准确确定某个值是否表示 <xref:System.Double.NaN?displayProperty=fullName> ，请使用 <xref:System.Single.IsNaN%2A?displayProperty=fullName> 或 <xref:System.Double.IsNaN%2A?displayProperty=fullName> 来测试值。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示两个表达式，这些表达式错误地测试值 <xref:System.Double.NaN?displayProperty=fullName> 和正确使用 <xref:System.Double.IsNaN%2A?displayProperty=fullName> 来测试值的表达式。

 [!code-csharp[FxCop.Usage.TestForNaN#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/cs/FxCop.Usage.TestForNaN.cs#1)]
 [!code-vb[FxCop.Usage.TestForNaN#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/vb/FxCop.Usage.TestForNaN.vb#1)]
