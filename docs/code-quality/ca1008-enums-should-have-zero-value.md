---
title: CA1008:枚举应具有零值
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1008
- EnumsShouldHaveZeroValue
helpviewer_keywords:
- CA1008
- EnumsShouldHaveZeroValue
ms.assetid: 3503a73c-360c-416d-8ee4-c2aa44365a05
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: c9b6e48fb82be5a41c420827a32926630bb725ed
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236494"
---
# <a name="ca1008-enums-should-have-zero-value"></a>CA1008:枚举应具有零值

|||
|-|-|
|TypeName|EnumsShouldHaveZeroValue|
|CheckId|CA1008|
|类别|Microsoft.Design|
|重大更改|不间断-当系统提示你向非标志枚举添加**无**值时。 如果系统提示重命名或删除任何枚举值，则为。|

## <a name="cause"></a>原因

没有应用<xref:System.FlagsAttribute?displayProperty=fullName>的枚举不会定义值为零的成员。 或者，已应用<xref:System.FlagsAttribute>的枚举定义了值为零但其名称不为 "None" 的成员。 或枚举定义多个零值成员。

默认情况下，此规则仅查看外部可见的枚举，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

与其他值类型一样，未初始化枚举的默认值为零。 非标志特性的枚举应定义值为零的成员，以便默认值为枚举的有效值。 如果需要，请将成员命名为 "None"。 否则，将零赋给最常使用的成员。 默认情况下，如果未在声明中设置第一个枚举成员的值，则其值为零。

如果应用了的<xref:System.FlagsAttribute>枚举定义了零值成员，则其名称应为 "None"，以指示枚举中未设置任何值。 将零值成员用于任何其他目的与<xref:System.FlagsAttribute>在中使用的不同之处在于，and 和 or 位运算符对成员没有意义。 这意味着，只应为一个成员分配值零。 如果有多个值为零的成员在标志特性的枚举中出现`Enum.ToString()` ，则将为不为零的成员返回不正确的结果。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与非标志属性枚举的此规则的冲突，请定义值为零的成员;这是非重大更改。 对于定义零值成员的标志属性枚举，请将此成员命名为 "None"，并删除值为零的任何其他成员;这是一项重大更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

请勿禁止显示此规则发出的警告，但之前已发布的标志特性化枚举除外。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1008.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（设计）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的示例演示两个满足规则的枚举和一个违反规则`BadTraceOptions`的枚举。

[!code-cpp[FxCop.Design.EnumsZeroValue#1](../code-quality/codesnippet/CPP/ca1008-enums-should-have-zero-value_1.cpp)]
[!code-csharp[FxCop.Design.EnumsZeroValue#1](../code-quality/codesnippet/CSharp/ca1008-enums-should-have-zero-value_1.cs)]
[!code-vb[FxCop.Design.EnumsZeroValue#1](../code-quality/codesnippet/VisualBasic/ca1008-enums-should-have-zero-value_1.vb)]

## <a name="related-rules"></a>相关规则

- [CA2217不要用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)
- [CA1700不要命名 "Reserved" 枚举值](../code-quality/ca1700-do-not-name-enum-values-reserved.md)
- [CA1712不要将类型名称作为枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)
- [CA1028枚举存储应为 Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)
- [CA1027用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>请参阅

- <xref:System.Enum?displayProperty=fullName>