---
title: CA1054：URI 参数不应为字符串
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1054
- UriParametersShouldNotBeStrings
helpviewer_keywords:
- CA1054
- UriParametersShouldNotBeStrings
ms.assetid: 8e99d72b-a658-47a7-8dd5-9784ce2c30b8
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 5f4efbec200b90614a5d78a4b04b2ebd32588cb5
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349076"
---
# <a name="ca1054-uri-parameters-should-not-be-strings"></a>CA1054：URI 参数不应为字符串

|||
|-|-|
|TypeName|UriParametersShouldNotBeStrings|
|CheckId|CA1054|
|类别|Microsoft. Design|
|重大更改|重大|

## <a name="cause"></a>原因

类型声明一个方法，该方法具有一个字符串参数，该字符串参数的名称中包含 "uri"、"Uri"、"urn"、"Urn"、"url" 或 "Url"，而类型未声明采用 <xref:System.Uri?displayProperty=fullName> 参数的对应重载。

默认情况下，此规则仅查看外部可见类型，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

此规则根据 camel 大小写约定将参数名称拆分为标记，并检查每个标记是否等于 "uri"、"Uri"、"urn"、"Urn"、"url" 或 "Url"。 如果有匹配项，则规则假定参数表示统一资源标识符（URI）。 URI 的字符串表示形式容易导致分析和编码错误，并且可造成安全漏洞。 如果方法采用 URI 的字符串表示形式，则应提供相应的重载，该重载采用 <xref:System.Uri> 类的实例，以安全、安全的方式提供这些服务。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请将参数更改为 @no__t 类型;这是一项重大更改。 或者，提供方法的重载，该重载采用 @no__t 的参数;这是非重大更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果参数不表示 URI，则可以安全地禁止显示此规则发出的警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1054.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（设计）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的示例显示了一个与此规则冲突的类型 `ErrorProne`，以及一个满足规则的类型（@no__t 为1）。

[!code-csharp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CSharp/ca1054-uri-parameters-should-not-be-strings_1.cs)]
[!code-vb[FxCop.Design.UriNotString#1](../code-quality/codesnippet/VisualBasic/ca1054-uri-parameters-should-not-be-strings_1.vb)]
[!code-cpp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CPP/ca1054-uri-parameters-should-not-be-strings_1.cpp)]

## <a name="related-rules"></a>相关规则

- [CA1056：URI 属性不应是字符串](../code-quality/ca1056-uri-properties-should-not-be-strings.md)
- [CA1055：URI 返回值不应是字符串](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
- [CA2234：传递 System.Uri 对象，而不传递字符串](../code-quality/ca2234.md)
- [CA1057：字符串 URI 重载调用 System.Uri 重载](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)