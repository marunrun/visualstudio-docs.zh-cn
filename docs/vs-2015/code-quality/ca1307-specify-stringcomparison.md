---
title: CA1307：指定 StringComparison |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1307
- SpecifyStringComparison
helpviewer_keywords:
- CA1307
- SpecifyStringComparison
ms.assetid: 9b0d5e71-1683-4a0d-bc4a-68b2fbd8af71
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 033d8f0e22ec040ffb10821993a5a9c647ee401e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538913"
---
# <a name="ca1307-specify-stringcomparison"></a>CA1307:指定 StringComparison
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|SpecifyStringComparison|
|CheckId|CA1307|
|Category|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 字符串比较操作使用未设置参数的方法重载 <xref:System.StringComparison> 。

## <a name="rule-description"></a>规则描述
 许多字符串操作（ <xref:System.String.Compare%2A> 和 <xref:System.String.Equals%2A> 方法）都提供接受 <xref:System.StringComparison> 枚举值作为参数的重载。

 只要存在采用参数的重载 <xref:System.StringComparison> ，就应该使用它而不是不采用此参数的重载。 通过显式设置此参数，你的代码通常会更清晰且更易于维护。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将字符串比较方法更改为接受 <xref:System.StringComparison> 枚举作为参数的重载。 例如：将更改 `String.Compare(str1, str2)` 为 `String.Compare(str1, str2, StringComparison.Ordinal)` 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果库或应用程序适用于受限制的本地受众，则可以安全地禁止显示此规则发出的警告，而不会对其进行本地化。

## <a name="see-also"></a>另请参阅
 [全球化警告](../code-quality/globalization-warnings.md) [CA1309：使用序数 StringComparison](../code-quality/ca1309-use-ordinal-stringcomparison.md)
