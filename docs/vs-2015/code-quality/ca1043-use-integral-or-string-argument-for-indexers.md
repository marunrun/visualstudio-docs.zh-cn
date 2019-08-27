---
title: CA1043:使用整型或字符串参数用于索引器 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 643d91ad51e9511bbd4440d2f84fbd441c768a53
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143216"
---
# <a name="ca1043-use-integral-or-string-argument-for-indexers"></a>CA1043:将整型或字符串参数用于索引器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseIntegralOrStringArgumentForIndexers|
|CheckId|CA1043|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型包含公共或受保护的索引器，而不使用索引类型<xref:System.Int32?displayProperty=fullName>， <xref:System.Int64?displayProperty=fullName>， <xref:System.Object?displayProperty=fullName>，或<xref:System.String?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 索引器，也就是说，索引属性，应为索引使用整数或字符串类型。 这些类型通常用于数据结构编制索引，并且提高库的可用性。 使用<xref:System.Object>类型应被限制为这种情况下，不能在设计时指定特定整型或字符串类型。 如果设计需要其他类型的索引，请重新考虑是否该类型表示逻辑数据存储区。 如果它不表示逻辑数据存储区，使用一种方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改索引为整数或字符串类型，或使用一种方法，而不是索引器。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 禁止显示此规则仅在仔细考虑要使用非标准索引器后的警告。

## <a name="example"></a>示例
 下面的示例演示使用的索引器<xref:System.Int32>索引。

 [!code-cpp[FxCop.Design.IntegralOrStringIndexers#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/cpp/FxCop.Design.IntegralOrStringIndexers.cpp#1)]
 [!code-csharp[FxCop.Design.IntegralOrStringIndexers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/cs/FxCop.Design.IntegralOrStringIndexers.cs#1)]
 [!code-vb[FxCop.Design.IntegralOrStringIndexers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/vb/FxCop.Design.IntegralOrStringIndexers.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1023:索引器不应是多维](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)

 [CA1024： 在适用处在适用处使用属性](../code-quality/ca1024-use-properties-where-appropriate.md)
