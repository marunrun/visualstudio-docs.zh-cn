---
title: CA1309：使用 ordinal StringComparison |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: be60d2a1dcb769a0b7a8574984de3d288bf57af4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538874"
---
# <a name="ca1309-use-ordinal-stringcomparison"></a>CA1309:使用按顺序的 StringComparison
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|UseOrdinalStringComparison|
|CheckId|CA1309|
|Category|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 Nonlinguistic 的字符串比较运算不会将 <xref:System.StringComparison> 参数设置为**Ordinal**或**stringcomparison.ordinalignorecase**。

## <a name="rule-description"></a>规则描述
 许多字符串运算，最重要的是 <xref:System.String.Compare%2A?displayProperty=fullName> 和 <xref:System.String.Equals%2A?displayProperty=fullName> 方法，现在提供接受 <xref:System.StringComparison?displayProperty=fullName> 枚举值作为参数的重载。

 指定**StringComparison**或**StringComparison**时，字符串比较将为 nonlinguistic。 也就是说，在进行比较决策时，将忽略特定于自然语言的功能。 这意味着决策基于简单的字节比较，并忽略由区域性参数化的大小写或相等表。 因此，通过将参数显式设置为**StringComparison**或**StringComparison**，你的代码通常会获得速度、提高正确性，并变得更可靠。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将字符串比较方法更改为接受 <xref:System.StringComparison?displayProperty=fullName> 枚举作为参数的重载，并指定**序数**或**stringcomparison.ordinalignorecase**。 例如，将 `String.Compare(str1, str2)` 更改为 `String.Compare(str1, str2, StringComparison.Ordinal)`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果库或应用程序适用于受限制的本地受众或应使用当前区域性的语义，则可以安全地禁止显示此规则发出的警告。

## <a name="see-also"></a>另请参阅
 [全球化警告](../code-quality/globalization-warnings.md) [CA1307：指定 StringComparison](../code-quality/ca1307-specify-stringcomparison.md)
