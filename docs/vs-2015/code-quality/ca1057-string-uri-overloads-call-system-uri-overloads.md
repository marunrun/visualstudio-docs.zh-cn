---
title: CA1057:字符串 URI 重载调用 System.Uri 重载 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1057
- StringUriOverloadsCallSystemUriOverloads
helpviewer_keywords:
- StringUriOverloadsCallSystemUriOverloads
- CA1057
ms.assetid: ef1e983e-9ca7-404b-82d7-65740ba0ce20
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4cf50ca225544b06409415320c73e7824a10843a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552724"
---
# <a name="ca1057-string-uri-overloads-call-systemuri-overloads"></a>CA1057:字符串 URI 重载调用 System.Uri 重载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 一种类型声明的差异仅在于替换的字符串参数的方法重载<xref:System.Uri?displayProperty=fullName>参数，并采用字符串参数的重载不会调用的重载的<xref:System.Uri>参数。

## <a name="rule-description"></a>规则说明
 因为重载的区别仅由字符串 /<xref:System.Uri>参数，则假定该字符串来表示统一资源标识符 (URI)。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 <xref:System.Uri>类以安全的方式提供这些服务。 若要获得的好处<xref:System.Uri>类，字符串重载应调用<xref:System.Uri>重载使用字符串自变量。

## <a name="how-to-fix-violations"></a>如何解决冲突
 重新实现的方法，使其创建的实例使用的 uri 的字符串表示形式<xref:System.Uri>类使用的字符串参数，并随后将传递<xref:System.Uri>对象的重载都<xref:System.Uri>参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果字符串参数不表示一个 URI。

## <a name="example"></a>示例
 下面的示例显示了正确实现的字符串重载。

 [!code-cpp[FxCop.Design.CallUriOverload#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cpp/FxCop.Design.CallUriOverload.cpp#1)]
 [!code-csharp[FxCop.Design.CallUriOverload#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cs/FxCop.Design.CallUriOverload.cs#1)]
 [!code-vb[FxCop.Design.CallUriOverload#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/vb/FxCop.Design.CallUriOverload.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2234:传递 System.Uri 对象，而不是字符串](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1056:URI 属性不应为字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054:URI 参数不应为字符串](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055:URI 返回值不应为字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
