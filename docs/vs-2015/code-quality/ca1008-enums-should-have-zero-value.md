---
title: CA1008：枚举应具有零值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1008
- EnumsShouldHaveZeroValue
helpviewer_keywords:
- CA1008
- EnumsShouldHaveZeroValue
ms.assetid: 3503a73c-360c-416d-8ee4-c2aa44365a05
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ca58938a55330243315529e9c7990b59d1a6fe5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548338"
---
# <a name="ca1008-enums-should-have-zero-value"></a>CA1008:枚举应具有零值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|EnumsShouldHaveZeroValue|
|CheckId|CA1008|
|Category|Microsoft. Design|
|是否重大更改|不间断-当系统提示你向非标志枚举添加**无**值时。如果系统提示重命名或删除任何枚举值，则为。|

## <a name="cause"></a>原因
 未应用的枚举 <xref:System.FlagsAttribute?displayProperty=fullName> 未定义值为零的成员; 或已应用的枚举 <xref:System.FlagsAttribute> 定义了值为零但其名称不为 "None" 的成员，或者枚举定义了多个零值成员。

## <a name="rule-description"></a>规则描述
 与其他值类型一样，未初始化枚举的默认值为零。 非标志−特性化枚举应定义值为零的成员，以便默认值为枚举的有效值。 如果需要，请将成员命名为 "None"。 否则，将零赋给最常使用的成员。 请注意，默认情况下，如果未在声明中设置第一个枚举成员的值，则其值为零。

 如果应用了的枚举 <xref:System.FlagsAttribute> 定义了零值成员，则其名称应为 "None"，以指示枚举中未设置任何值。 将零值成员用于任何其他目的与在中使用的不同之处在于， <xref:System.FlagsAttribute> and 和 or 位运算符对成员没有意义。 这意味着，只应为一个成员分配值零。 请注意，如果具有值零的多个成员在标志特性枚举中出现，则 `Enum.ToString()` 会为非零成员返回不正确的结果。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复非标志−特性化枚举的此规则的冲突，请定义值为零的成员;这是非重大更改。 对于定义零值成员的标志属性枚举，请将此成员命名为 "None"，并删除值为零的任何其他成员;这是一项重大更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，但之前已发布的标志特性化枚举除外。

## <a name="example"></a>示例
 下面的示例演示两个满足规则的枚举和一个 `BadTraceOptions` 违反规则的枚举。

 [!code-cpp[FxCop.Design.EnumsZeroValue#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/cpp/FxCop.Design.EnumsZeroValue.cpp#1)]
 [!code-csharp[FxCop.Design.EnumsZeroValue#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/cs/FxCop.Design.EnumsZeroValue.cs#1)]
 [!code-vb[FxCop.Design.EnumsZeroValue#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/vb/FxCop.Design.EnumsZeroValue.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2217:不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

 [CA1700:不要命名“Reserved”枚举值](../code-quality/ca1700-do-not-name-enum-values-reserved.md)

 [CA1712:不要将类型名用作枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

 [CA1028:枚举存储应为 Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

 [CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Enum?displayProperty=fullName>
