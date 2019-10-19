---
title: CA2241：为格式化方法提供正确的参数 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 112065b2a8b9a88241ce62dda7b32a2f2c22fc75
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672024"
---
# <a name="ca2241-provide-correct-arguments-to-formatting-methods"></a>CA2241：为格式化方法提供正确的自变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ProvideCorrectArgumentsToFormattingMethods|
|CheckId|CA2241|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 传递给方法的 `format` 字符串参数 <xref:System.Console.WriteLine%2A>、<xref:System.Console.Write%2A> 或 <xref:System.String.Format%2A?displayProperty=fullName> 不包含对应于每个对象参数的格式项，反之亦然。

## <a name="rule-description"></a>规则说明
 方法的参数（例如 <xref:System.Console.WriteLine%2A>、<xref:System.Console.Write%2A> 和 <xref:System.String.Format%2A>）包含格式字符串，后跟多个 <xref:System.Object?displayProperty=fullName> 实例。 格式字符串包含格式为 {index [，对齐方式] [：格式表]} 的文本和嵌入格式项。 “index”是一个从零开始的整数，用于指示要格式化的对象。 如果对象在格式字符串中没有相应的索引，则忽略该对象。 如果 "index" 指定的对象不存在，则在运行时将引发 <xref:System.FormatException?displayProperty=fullName>。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请为每个对象参数提供一个格式项，并为每个格式项提供一个对象参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了两个规则冲突。

 [!code-csharp[FxCop.Usage.FormattingArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/cs/FxCop.Usage.FormattingArguments.cs#1)]
 [!code-vb[FxCop.Usage.FormattingArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/vb/FxCop.Usage.FormattingArguments.vb#1)]
