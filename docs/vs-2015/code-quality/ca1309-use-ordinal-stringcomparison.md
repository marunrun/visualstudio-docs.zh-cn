---
title: CA1309:使用序号 StringComparison |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseOrdinalStringComparison
- CA1309
helpviewer_keywords:
- UseOrdinalStringComparison
- CA1309
ms.assetid: 19be0854-cb6e-4efd-a4c8-a5c1fc6f7a71
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7b491cf06528b67c96f90f314210e61800e0cab1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200339"
---
# <a name="ca1309-use-ordinal-stringcomparison"></a>CA1309:使用按顺序的 StringComparison
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseOrdinalStringComparison|
|CheckId|CA1309|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 非语义字符串比较操作不会设置<xref:System.StringComparison>为参数**序号**或**OrdinalIgnoreCase**。

## <a name="rule-description"></a>规则说明
 许多字符串运算，最重要<xref:System.String.Compare%2A?displayProperty=fullName>并<xref:System.String.Equals%2A?displayProperty=fullName>方法，现在提供一个重载接受<xref:System.StringComparison?displayProperty=fullName>枚举作为参数的值。

 当您指定**StringComparison.Ordinal**或**StringComparison.OrdinalIgnoreCase**，将非语义字符串比较。 也就是说，进行比较的决策时，将忽略特定于自然语言的功能。 这意味着决策基于简单的字节比较，并且忽略大小写或相等表是按区域性参数化。 因此，通过将参数显式设置为**StringComparison.Ordinal**或**StringComparison.OrdinalIgnoreCase**，你的代码通常获得速度、 提高正确性，并变得更可靠。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请将字符串比较方法更改为重载接受<xref:System.StringComparison?displayProperty=fullName>枚举作为参数，并指定**序号**或**OrdinalIgnoreCase**。 例如，将 `String.Compare(str1, str2)` 更改为 `String.Compare(str1, str2, StringComparison.Ordinal)`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，当库或应用程序旨在为有限的本地用户或应使用当前区域性的语义。

## <a name="see-also"></a>请参阅
 [全球化警告](../code-quality/globalization-warnings.md) [CA1307:指定 StringComparison](../code-quality/ca1307-specify-stringcomparison.md)
