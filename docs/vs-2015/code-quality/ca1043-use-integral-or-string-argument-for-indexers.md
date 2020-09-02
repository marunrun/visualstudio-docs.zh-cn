---
title: CA1043：将整型或字符串参数用于索引器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
helpviewer_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
ms.assetid: d7f14b9e-2220-4f80-b6b8-48c655a05701
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03d21a824d2d3a9151dad139575f32e3417cbd39
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546830"
---
# <a name="ca1043-use-integral-or-string-argument-for-indexers"></a>CA1043:将整型或字符串参数用于索引器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|UseIntegralOrStringArgumentForIndexers|
|CheckId|CA1043|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型包含一个公共或受保护索引器，该索引器使用除 <xref:System.Int32?displayProperty=fullName> 、 <xref:System.Int64?displayProperty=fullName> 、或之外的索引类型 <xref:System.Object?displayProperty=fullName> <xref:System.String?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 索引器（即索引属性）应将整型或字符串类型用于索引。 这些类型通常用于索引数据结构并提高库的可用性。 <xref:System.Object>应将类型的使用限制为在设计时无法指定特定整数或字符串类型的情况。 如果设计需要索引的其他类型，请重新考虑该类型是否表示逻辑数据存储区。 如果它不表示逻辑数据存储，请使用方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将索引更改为整数或字符串类型，或者使用方法而不是索引器。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅在仔细考虑非标准索引器的需求之后，禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个使用索引的索引器 <xref:System.Int32> 。

 [!code-cpp[FxCop.Design.IntegralOrStringIndexers#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/cpp/FxCop.Design.IntegralOrStringIndexers.cpp#1)]
 [!code-csharp[FxCop.Design.IntegralOrStringIndexers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/cs/FxCop.Design.IntegralOrStringIndexers.cs#1)]
 [!code-vb[FxCop.Design.IntegralOrStringIndexers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/vb/FxCop.Design.IntegralOrStringIndexers.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1023:索引器不应是多维的](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)

 [CA1024:在适用处使用属性](../code-quality/ca1024-use-properties-where-appropriate.md)
