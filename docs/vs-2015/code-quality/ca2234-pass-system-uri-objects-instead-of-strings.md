---
title: CA2234：传递 System.object 对象而不是字符串 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PassSystemUriObjectsInsteadOfStrings
- CA2234
helpviewer_keywords:
- CA2234
- PassSystemUriObjectsInsteadOfStrings
ms.assetid: 14616b37-74c4-4286-b051-115d00aceb5f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ce5c076260886def089118a4d7211d75e0185c0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545205"
---
# <a name="ca2234-pass-systemuri-objects-instead-of-strings"></a>CA2234:传递 System.Uri 对象，而不传递字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|PassSystemUriObjectsInsteadOfStrings|
|CheckId|CA2234|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 调用了一个方法，该方法具有一个字符串参数，该参数的名称包含 "uri"、"Uri"、"urn"、"Urn"、"url" 或 "Url";方法的声明类型包含一个具有参数的对应方法重载 <xref:System.Uri?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 参数名称根据 camel 大小写约定拆分为标记，然后检查每个标记，以查看其是否等于 "uri"、"Uri"、"urn"、"Urn"、"url" 或 "Url"。 如果存在匹配项，则假定参数表示统一资源标识符（URI）。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 <xref:System.Uri>类以安全安全的方式提供这些服务。 如果在两个重载之间进行选择，而这两个重载只是与 URI 的表示形式不同，则用户应选择采用 <xref:System.Uri> 自变量的重载。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请调用采用参数的重载 <xref:System.Uri> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果 string 参数不表示 URI，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了一个方法， `ErrorProne` 该方法违反了规则和 `SaferWay` 正确调用重载的方法 <xref:System.Uri> 。

 [!code-cpp[FxCop.Usage.PassUri#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/cpp/FxCop.Usage.PassUri.cpp#1)]
 [!code-csharp[FxCop.Usage.PassUri#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/cs/FxCop.Usage.PassUri.cs#1)]
 [!code-vb[FxCop.Usage.PassUri#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/vb/FxCop.Usage.PassUri.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1057:字符串 URI 重载调用 System.Uri 重载](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)

 [CA1056:URI 属性不应是字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054:URI 参数不应为字符串](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055:URI 返回值不应是字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
