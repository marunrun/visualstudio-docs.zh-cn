---
title: CA1054:URI 参数不应是字符串 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f7af579cf92a785f9850805ae06743a15364eade
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200525"
---
# <a name="ca1054-uri-parameters-should-not-be-strings"></a>CA1054:URI 参数不应为字符串
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UriParametersShouldNotBeStrings|
|CheckId|CA1054|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 某个类型声明具有其名称包含"uri"、"Uri"、"urn"、"Urn"、"url"或"Url"的字符串参数的方法和类型没有声明的相应重载采用<xref:System.Uri?displayProperty=fullName>参数。

## <a name="rule-description"></a>规则说明
 此规则将参数名称拆分为令牌基于驼峰式大小写约定，并检查每个令牌等于"uri"、"Uri"、"urn"、"Urn"、"url"或"Url"。 如果没有匹配项，该规则将假定该参数表示统一资源标识符 (URI)。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 如果某方法采用 URI 的字符串表示形式，提供采用的实例应为相应重载<xref:System.Uri>类，以安全的方式提供这些服务。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，将参数更改为<xref:System.Uri>类型; 这是一项重大更改。 或者，提供它采用的方法的重载<xref:System.Uri>参数; 这是中断性更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果该参数不表示一个 URI。

## <a name="example"></a>示例
 下面的示例演示一种类型， `ErrorProne`，这违反了此规则和一个类型， `SaferWay`，满足该规则。

 [!code-cpp[FxCop.Design.UriNotString#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cpp/FxCop.Design.UriNotString.cpp#1)]
 [!code-csharp[FxCop.Design.UriNotString#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cs/FxCop.Design.UriNotString.cs#1)]
 [!code-vb[FxCop.Design.UriNotString#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/vb/FxCop.Design.UriNotString.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1056:URI 属性不应为字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1055:URI 返回值不应为字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)

 [CA2234:传递 System.Uri 对象，而不是字符串](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1057:字符串 URI 重载调用 System.Uri 重载](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)
