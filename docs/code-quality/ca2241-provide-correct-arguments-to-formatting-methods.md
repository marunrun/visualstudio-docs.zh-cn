---
title: CA2241:为格式化方法提供正确的参数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2241
- Provide correct arguments to formatting methods
- ProvideCorrectArgumentsToFormattingMethods
helpviewer_keywords:
- ProvideCorrectArgumentsToFormattingMethods
- CA2241
ms.assetid: 83639bc4-4c91-4a07-a40e-dc5e49a84494
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 10a4cdaa1e2de768cadc569424a490aa4adb7135
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253217"
---
# <a name="ca2241-provide-correct-arguments-to-formatting-methods"></a>CA2241:为格式化方法提供正确的参数

|||
|-|-|
|TypeName|ProvideCorrectArgumentsToFormattingMethods|
|CheckId|CA2241|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因
传递给方法<xref:System.Console.WriteLine%2A>（如、 <xref:System.Console.Write%2A>或<xref:System.String.Format%2A?displayProperty=fullName> ）的字符串参数不包含对应于每个对象参数的格式项，反之亦然。`format`

## <a name="rule-description"></a>规则说明
方法<xref:System.Console.WriteLine%2A>（如、和<xref:System.String.Format%2A> ）的<xref:System.Console.Write%2A>参数包含格式字符串，后跟若干个<xref:System.Object?displayProperty=fullName>实例。 格式字符串包含格式为 {index [，对齐方式] [：格式表]} 的文本和嵌入格式项。 “index”是一个从零开始的整数，用于指示要格式化的对象。 如果对象在格式字符串中没有相应的索引，则忽略该对象。 如果 "index" 指定的对象不存在， <xref:System.FormatException?displayProperty=fullName>则会在运行时引发。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请为每个对象参数提供一个格式项，并为每个格式项提供一个对象参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例显示了两个规则冲突。

[!code-vb[FxCop.Usage.FormattingArguments#1](../code-quality/codesnippet/VisualBasic/ca2241-provide-correct-arguments-to-formatting-methods_1.vb)]
[!code-csharp[FxCop.Usage.FormattingArguments#1](../code-quality/codesnippet/CSharp/ca2241-provide-correct-arguments-to-formatting-methods_1.cs)]