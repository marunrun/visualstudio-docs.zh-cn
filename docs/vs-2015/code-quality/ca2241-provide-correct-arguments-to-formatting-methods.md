---
title: CA2241:提供正确的自变量为格式化方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2241
- Provide correct arguments to formatting methods
- ProvideCorrectArgumentsToFormattingMethods
helpviewer_keywords:
- ProvideCorrectArgumentsToFormattingMethods
- CA2241
ms.assetid: 83639bc4-4c91-4a07-a40e-dc5e49a84494
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0a139db3fb1ece41c1d3f18471a286c72a7a576c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201516"
---
# <a name="ca2241-provide-correct-arguments-to-formatting-methods"></a>CA2241:为格式化方法提供正确的参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ProvideCorrectArgumentsToFormattingMethods|
|CheckId|CA2241|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 `format`字符串参数传递给方法，如<xref:System.Console.WriteLine%2A>， <xref:System.Console.Write%2A>，或<xref:System.String.Format%2A?displayProperty=fullName>不包含对应到每个对象自变量，或执行相反的格式项。

## <a name="rule-description"></a>规则说明
 等方法的参数<xref:System.Console.WriteLine%2A>， <xref:System.Console.Write%2A>，并<xref:System.String.Format%2A>包含多个后跟一个格式字符串<xref:System.Object?displayProperty=fullName>实例。 格式字符串包含文本和嵌入的格式项的窗体中，{索引 [，对齐方式] [: formatString]}。 “index”是一个从零开始的整数，用于指示要格式化的对象。 如果对象在格式字符串中没有对应的索引，则忽略该对象。 如果指定 index 的对象不存在，<xref:System.FormatException?displayProperty=fullName>在运行时引发。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请为每个对象自变量提供的格式项并提供每个格式项的对象参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示两个规则的冲突。

 [!code-csharp[FxCop.Usage.FormattingArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/cs/FxCop.Usage.FormattingArguments.cs#1)]
 [!code-vb[FxCop.Usage.FormattingArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/vb/FxCop.Usage.FormattingArguments.vb#1)]
