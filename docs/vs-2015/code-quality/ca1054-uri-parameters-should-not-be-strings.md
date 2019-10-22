---
title: CA1054： URI 参数不应为字符串 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1054
- UriParametersShouldNotBeStrings
helpviewer_keywords:
- CA1054
- UriParametersShouldNotBeStrings
ms.assetid: 8e99d72b-a658-47a7-8dd5-9784ce2c30b8
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2062c7518545300074a0377b7a9cca7ddf1a8aa5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603369"
---
# <a name="ca1054-uri-parameters-should-not-be-strings"></a>CA1054：URI 参数不应为字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UriParametersShouldNotBeStrings|
|CheckId|CA1054|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型声明一个方法，该方法具有一个字符串参数，该字符串参数的名称中包含 "uri"、"Uri"、"urn"、"Urn"、"url" 或 "Url"，而类型未声明采用 <xref:System.Uri?displayProperty=fullName> 参数的对应重载。

## <a name="rule-description"></a>规则说明
 此规则根据 camel 大小写约定将参数名称拆分为标记，并检查每个标记是否等于 "uri"、"Uri"、"urn"、"Urn"、"url" 或 "Url"。 如果有匹配项，则规则假定参数表示统一资源标识符（URI）。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 如果方法采用 URI 的字符串表示形式，则应提供相应的重载，该重载采用 <xref:System.Uri> 类的实例，以安全、安全的方式提供这些服务。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将参数更改为 <xref:System.Uri> 类型;这是一项重大更改。 或者，提供方法的重载，该重载采用 <xref:System.Uri> 参数;这是一种不间断更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果参数不表示 URI，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了违反此规则的类型 `ErrorProne`，以及满足规则的类型 `SaferWay`。

 [!code-cpp[FxCop.Design.UriNotString#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cpp/FxCop.Design.UriNotString.cpp#1)]
 [!code-csharp[FxCop.Design.UriNotString#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cs/FxCop.Design.UriNotString.cs#1)]
 [!code-vb[FxCop.Design.UriNotString#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/vb/FxCop.Design.UriNotString.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1056：URI 属性不应是字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1055：URI 返回值不应是字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)

 [CA2234：传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1057：字符串 URI 重载调用 System.Uri 重载](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)
