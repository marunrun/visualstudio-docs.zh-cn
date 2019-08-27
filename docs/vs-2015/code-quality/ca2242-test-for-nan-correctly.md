---
title: CA2242:正确测试 NaN |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 17a98ce3d213c5d9ae85bb5132a0a44e50112037
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142355"
---
# <a name="ca2242-test-for-nan-correctly"></a>CA2242:正确测试 NaN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TestForNaNCorrectly|
|CheckId|CA2242|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 一个表达式测试值与<xref:System.Single.NaN?displayProperty=fullName>或<xref:System.Double.NaN?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 <xref:System.Double.NaN?displayProperty=fullName>这表示未一个数字，结果时未定义的算术运算。 任何表达式，以便测试在值之间的相等性和<xref:System.Double.NaN?displayProperty=fullName>始终返回`false`。 任何表达式，以便测试在值之间的不相等并<xref:System.Double.NaN?displayProperty=fullName>始终返回`true`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，并准确地确定某个值是否表示<xref:System.Double.NaN?displayProperty=fullName>，使用<xref:System.Single.IsNaN%2A?displayProperty=fullName>或<xref:System.Double.IsNaN%2A?displayProperty=fullName>来测试值。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示两个错误地测试对值的表达式<xref:System.Double.NaN?displayProperty=fullName>和正确使用的表达式，<xref:System.Double.IsNaN%2A?displayProperty=fullName>来测试值。

 [!code-csharp[FxCop.Usage.TestForNaN#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/cs/FxCop.Usage.TestForNaN.cs#1)]
 [!code-vb[FxCop.Usage.TestForNaN#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.TestForNaN/vb/FxCop.Usage.TestForNaN.vb#1)]
