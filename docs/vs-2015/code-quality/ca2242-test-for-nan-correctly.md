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
ms.openlocfilehash: 8433ac081a45e3dbab80ffcd6f96e6d1db914337
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672010"
---
# <a name="ca2242-test-for-nan-correctly"></a>CA2242：正确测试 NaN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TestForNaNCorrectly|
|CheckId|CA2242|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 表达式根据 <xref:System.Single.NaN?displayProperty=fullName> 或 <xref:System.Double.NaN?displayProperty=fullName> 测试值。

## <a name="rule-description"></a>规则说明
 如果未定义算术运算，则 <xref:System.Double.NaN?displayProperty=fullName> （表示非数字）。 测试值和 <xref:System.Double.NaN?displayProperty=fullName> 之间相等性的任何表达式始终返回 `false`。 测试值和 <xref:System.Double.NaN?displayProperty=fullName> 之间不相等的任何表达式始终返回 `true`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，并准确确定某个值是否表示 <xref:System.Double.NaN?displayProperty=fullName>，请使用 <xref:System.Single.IsNaN%2A?displayProperty=fullName> 或 <xref:System.Double.IsNaN%2A?displayProperty=fullName> 来测试值。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示两个表达式，这些表达式不正确地针对 <xref:System.Double.NaN?displayProperty=fullName> 和正确使用 <xref:System.Double.IsNaN%2A?displayProperty=fullName> 测试值的表达式进行测试。

 [!code-csharp[FxCop.Usage.TestForNaN#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/cs/FxCop.Usage.TestForNaN.cs#1)]
 [!code-vb[FxCop.Usage.TestForNaN#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/vb/FxCop.Usage.TestForNaN.vb#1)]
