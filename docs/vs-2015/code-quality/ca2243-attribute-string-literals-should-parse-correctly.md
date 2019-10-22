---
title: CA2243：应正确分析特性字符串文本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2243
- AttributeStringLiteralsShouldParseCorrectly
helpviewer_keywords:
- AttributeStringLiteralsShouldParseCorrectly
- CA2243
ms.assetid: bfadb366-379d-4ee4-b17b-c4a09bf1106b
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 62a2adc6f01e5cb26a6af26d71a124f8b81e07fb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671968"
---
# <a name="ca2243-attribute-string-literals-should-parse-correctly"></a>CA2243：应正确分析特性字符串文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AttributeStringLiteralsShouldParseCorrectly|
|CheckId|CA2243|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 对于 URL、GUID 或版本，无法正确分析特性的字符串文本参数。

## <a name="rule-description"></a>规则说明
 由于属性派生自 <xref:System.Attribute?displayProperty=fullName>，并且在编译时使用特性，因此只能将常数值传递给其构造函数。 必须表示 Url、Guid 和版本的属性参数不能类型化为 <xref:System.Uri?displayProperty=fullName>、<xref:System.Guid?displayProperty=fullName> 和 <xref:System.Version?displayProperty=fullName>，因为这些类型不能表示为常量。 相反，它们必须由字符串表示。

 由于参数已类型化为字符串，因此可能会在编译时传递格式不正确的参数。

 此规则使用命名试探法查找表示统一资源标识符（URI）、全局唯一标识符（GUID）或版本的参数，并验证所传递的值是否正确。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将参数字符串更改为格式正确的 URL、GUID 或版本。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果参数不表示 URL、GUID 或版本，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了与此规则冲突的 AssemblyFileVersionAttribute 的代码。

 [!code-csharp[FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly/cs/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly.cs#1)]

 规则由以下各项触发：

- 包含 "version" 的参数，不能分析为版本。

- 包含 "guid" 的参数，不能将其分析为 Guid.empty。

- 不能将包含 "uri"、"urn" 或 "url" 的参数解析为 system.string。

## <a name="see-also"></a>请参阅
 [CA1054：URI 参数不应为字符串](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)
