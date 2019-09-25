---
title: CA1028:枚举存储应为 Int32
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1028
- EnumStorageShouldBeInt32
helpviewer_keywords:
- EnumStorageShouldBeInt32
- CA1028
ms.assetid: 87160825-9f39-4142-8d7f-a31fe7ac7b84
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 47a934a6e35296927eea64465ff8e7007219bec5
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236084"
---
# <a name="ca1028-enum-storage-should-be-int32"></a>CA1028:枚举存储应为 Int32

|||
|-|-|
|TypeName|EnumStorageShouldBeInt32|
|CheckId|CA1028|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因

枚举的基础类型不<xref:System.Int32?displayProperty=fullName>是。

默认情况下，此规则仅查看公共枚举，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

枚举是一种值类型，它定义一组相关的已命名常数。 默认情况下， <xref:System.Int32?displayProperty=fullName>数据类型用于存储常量值。 尽管你可以更改此基础类型，但在大多数情况下不需要或建议使用此类型。 使用小于的数据类型<xref:System.Int32>，不会显著提高性能。 如果无法使用默认数据类型，则应使用符合公共语言系统（CLS）的整数<xref:System.Byte>类型（ <xref:System.Int32>、 <xref:System.Int16>、或<xref:System.Int64> ），以确保枚举的所有值都可以在中表示符合 CLS 的编程语言。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，除非存在大小或兼容性问题<xref:System.Int32>，否则请使用。 对于不太<xref:System.Int32>大而无法保存值的情况，请使用<xref:System.Int64>。 如果向后兼容性要求较小的数据<xref:System.Byte>类型<xref:System.Int16>，请使用或。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当后向兼容性问题需要时，才禁止显示此规则发出的警告。 在应用程序中，未能遵守此规则通常不会导致问题。 在需要语言互操作性的库中，未能遵守此规则可能会对用户造成不利影响。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1028.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（设计）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example-of-a-violation"></a>冲突示例

下面的示例演示两个不使用建议的基础数据类型的枚举。

[!code-vb[FxCop.Design.EnumIntegralType#1](../code-quality/codesnippet/VisualBasic/ca1028-enum-storage-should-be-int32_1.vb)]
[!code-csharp[FxCop.Design.EnumIntegralType#1](../code-quality/codesnippet/CSharp/ca1028-enum-storage-should-be-int32_1.cs)]

## <a name="example-of-how-to-fix"></a>解决方法的示例

下面的示例通过将基础数据类型更改为来<xref:System.Int32>修复前面的冲突。

[!code-csharp[FxCop.Design.EnumIntegralTypeFixed#1](../code-quality/codesnippet/CSharp/ca1028-enum-storage-should-be-int32_2.cs)]
[!code-vb[FxCop.Design.EnumIntegralTypeFixed#1](../code-quality/codesnippet/VisualBasic/ca1028-enum-storage-should-be-int32_2.vb)]

## <a name="related-rules"></a>相关规则

- [CA1008枚举应具有零值](../code-quality/ca1008-enums-should-have-zero-value.md)
- [CA1027用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
- [CA2217不要用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)
- [CA1700不要命名 "Reserved" 枚举值](../code-quality/ca1700-do-not-name-enum-values-reserved.md)
- [CA1712不要将类型名称作为枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

## <a name="see-also"></a>请参阅

- <xref:System.Byte?displayProperty=fullName>
- <xref:System.Int16?displayProperty=fullName>
- <xref:System.Int32?displayProperty=fullName>
- <xref:System.Int64?displayProperty=fullName>