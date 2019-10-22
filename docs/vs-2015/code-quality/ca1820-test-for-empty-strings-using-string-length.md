---
title: CA1820：使用字符串长度测试是否有空字符串 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
helpviewer_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
ms.assetid: da1e70c8-b1dc-46b9-8b8f-4e6e48339681
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6711dac907de2777cf892b20269fec7e99d3bd6f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657495"
---
# <a name="ca1820-test-for-empty-strings-using-string-length"></a>CA1820：使用字符串长度测试是否有空字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TestForEmptyStringsUsingStringLength|
|CheckId|CA1820|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 使用 <xref:System.Object.Equals%2A?displayProperty=fullName> 将字符串与空字符串进行比较。

## <a name="rule-description"></a>规则说明
 使用 <xref:System.String.Length%2A?displayProperty=fullName> 属性或 <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName> 方法比较字符串比使用 <xref:System.Object.Equals%2A> 明显快。 这是因为 <xref:System.Object.Equals%2A> 比 <xref:System.String.IsNullOrEmpty%2A> 或执行的指令数更多地执行多个 MSIL 指令，以检索 <xref:System.String.Length%2A> 属性值并将其与零进行比较。

 应当注意，对于 null 字符串，<xref:System.Object.Equals%2A> 和 <xref:System.String.Length%2A> = = 0 的行为不同。 如果尝试获取 null 字符串的 <xref:System.String.Length%2A> 属性的值，则公共语言运行时将引发 <xref:System.NullReferenceException?displayProperty=fullName>。 如果在空字符串和空字符串之间执行比较，则公共语言运行时不会引发异常;比较返回 `false`。 测试 null 不会对这两种方法的相对性能产生显著影响。 面向 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 时，请使用 <xref:System.String.IsNullOrEmpty%2A> 方法。 否则，请尽可能使用 <xref:System.String.Length%2A> = = 比较。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将比较更改为使用 <xref:System.String.Length%2A> 属性，并测试是否为 null 字符串。 如果目标 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]，请使用 <xref:System.String.IsNullOrEmpty%2A> 方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果性能不是问题，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了用于查找空字符串的不同技术。

 [!code-csharp[FxCop.Performance.StringTest#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.StringTest/cs/FxCop.Performance.StringTest.cs#1)]
