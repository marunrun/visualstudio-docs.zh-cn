---
title: CA1057:字符串 URI 重载调用 System.Uri 重载
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1057
- StringUriOverloadsCallSystemUriOverloads
helpviewer_keywords:
- StringUriOverloadsCallSystemUriOverloads
- CA1057
ms.assetid: ef1e983e-9ca7-404b-82d7-65740ba0ce20
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: e6bd77a49690979ea7ab3c4619fdd578a80bb77c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235512"
---
# <a name="ca1057-string-uri-overloads-call-systemuri-overloads"></a>CA1057:字符串 URI 重载调用 System.Uri 重载

|||
|-|-|
|TypeName|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因

类型声明仅通过将字符串参数替换为<xref:System.Uri?displayProperty=fullName>参数而有所不同的方法重载，而采用字符串参数的重载不调用<xref:System.Uri>采用参数的重载。

## <a name="rule-description"></a>规则说明
由于重载只是字符串或<xref:System.Uri>参数的不同之处，因此假定字符串表示统一资源标识符（URI）。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 <xref:System.Uri>类以安全安全的方式提供这些服务。 为了获得<xref:System.Uri>类的优点，字符串重载应使用字符串参数<xref:System.Uri>调用重载。

## <a name="how-to-fix-violations"></a>如何解决冲突
重新实现使用 URI 的字符串表示形式的方法，以便它使用字符串参数创建<xref:System.Uri>类的实例，然后将该<xref:System.Uri>对象传递给具有<xref:System.Uri>参数的重载。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果 string 参数不表示 URI，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示正确实现的字符串重载。

[!code-csharp[FxCop.Design.CallUriOverload#1](../code-quality/codesnippet/CSharp/ca1057-string-uri-overloads-call-system-uri-overloads_1.cs)]
[!code-cpp[FxCop.Design.CallUriOverload#1](../code-quality/codesnippet/CPP/ca1057-string-uri-overloads-call-system-uri-overloads_1.cpp)]
[!code-vb[FxCop.Design.CallUriOverload#1](../code-quality/codesnippet/VisualBasic/ca1057-string-uri-overloads-call-system-uri-overloads_1.vb)]

## <a name="related-rules"></a>相关规则
[CA2234传递 System.object 对象而不是字符串](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

[CA1056URI 属性不应是字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

[CA1054URI 参数不应为字符串](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

[CA1055URI 返回值不应是字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)