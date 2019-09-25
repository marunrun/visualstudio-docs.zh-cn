---
title: CA2242:正确测试 NaN
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TestForNaNCorrectly
- CA2242
helpviewer_keywords:
- CA2242
ms.assetid: e12dcffc-e255-4e1e-8fdf-3c6054d44abe
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 0e74ec49667a4fe66c399bd15e8b24aa6589ce88
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237843"
---
# <a name="ca2242-test-for-nan-correctly"></a>CA2242:正确测试 NaN

|||
|-|-|
|TypeName|TestForNaNCorrectly|
|CheckId|CA2242|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因
表达式根据<xref:System.Single.NaN?displayProperty=fullName>或<xref:System.Double.NaN?displayProperty=fullName>测试值。

## <a name="rule-description"></a>规则说明
 <xref:System.Double.NaN?displayProperty=fullName>如果未定义算术运算，则表示不是数字的结果。 测试值是否相等并<xref:System.Double.NaN?displayProperty=fullName>始终返回`false`的任何表达式。 对值进行不相等测试并<xref:System.Double.NaN?displayProperty=fullName>始终返回`true`的任何表达式。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，并准确确定某个值<xref:System.Double.NaN?displayProperty=fullName>是否表示<xref:System.Single.IsNaN%2A?displayProperty=fullName> ， <xref:System.Double.IsNaN%2A?displayProperty=fullName>请使用或来测试值。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示两个表达式，这些表达式错误地<xref:System.Double.NaN?displayProperty=fullName>测试值和正确使用<xref:System.Double.IsNaN%2A?displayProperty=fullName>来测试值的表达式。

[!code-vb[FxCop.Usage.TestForNaN#1](../code-quality/codesnippet/VisualBasic/ca2242-test-for-nan-correctly_1.vb)]
[!code-csharp[FxCop.Usage.TestForNaN#1](../code-quality/codesnippet/CSharp/ca2242-test-for-nan-correctly_1.cs)]