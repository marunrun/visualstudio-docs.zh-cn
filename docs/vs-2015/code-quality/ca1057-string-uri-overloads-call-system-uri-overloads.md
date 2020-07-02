---
title: CA1057：字符串 URI 重载调用 system.exception 重载 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bcdb4d8333b0a4d2d06580d882cf736d4527eca4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539524"
---
# <a name="ca1057-string-uri-overloads-call-systemuri-overloads"></a>CA1057:字符串 URI 重载调用 System.Uri 重载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型声明仅通过将字符串参数替换为参数而有所不同的方法重载 <xref:System.Uri?displayProperty=fullName> ，而采用字符串参数的重载不调用采用参数的重载 <xref:System.Uri> 。

## <a name="rule-description"></a>规则描述
 由于重载只是字符串/参数的不同之处 <xref:System.Uri> ，因此假定字符串表示统一资源标识符（URI）。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 <xref:System.Uri>类以安全安全的方式提供这些服务。 为了获得类的优点 <xref:System.Uri> ，字符串重载应 <xref:System.Uri> 使用字符串参数调用重载。

## <a name="how-to-fix-violations"></a>如何解决冲突
 重新实现使用 URI 的字符串表示形式的方法，以便它 <xref:System.Uri> 使用字符串参数创建类的实例，然后将该 <xref:System.Uri> 对象传递给具有参数的重载 <xref:System.Uri> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果 string 参数不表示 URI，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示正确实现的字符串重载。

 [!code-cpp[FxCop.Design.CallUriOverload#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cpp/FxCop.Design.CallUriOverload.cpp#1)]
 [!code-csharp[FxCop.Design.CallUriOverload#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cs/FxCop.Design.CallUriOverload.cs#1)]
 [!code-vb[FxCop.Design.CallUriOverload#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/vb/FxCop.Design.CallUriOverload.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2234:传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1056:URI 属性不应是字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054:URI 参数不应为字符串](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055:URI 返回值不应是字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
