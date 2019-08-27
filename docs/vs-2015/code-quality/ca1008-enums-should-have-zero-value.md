---
title: CA1008:枚举应具有零值 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e9b607c3a3fd7992bf8947c003d240d3d5b1d312
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182609"
---
# <a name="ca1008-enums-should-have-zero-value"></a>CA1008:枚举应具有零值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|EnumsShouldHaveZeroValue|
|CheckId|CA1008|
|类别|Microsoft.Design|
|是否重大更改|无间断-当系统提示添加**None**非标志枚举的值。是-当系统提示重命名或删除任何枚举值。|

## <a name="cause"></a>原因
 一个枚举，而无需应用<xref:System.FlagsAttribute?displayProperty=fullName>不会定义一个具有值为零; 或已应用的枚举的成员<xref:System.FlagsAttribute>定义了一个成员，其值为零，但其名称不是 'None' 或枚举定义多个零值成员。

## <a name="rule-description"></a>规则说明
 未初始化枚举，就像其他值类型的默认值为零。 无标志特性的枚举应定义了值为零，因此，默认值是有效的值的枚举的成员。 如果适当，命名为成员 None。 否则，将分配 0 到最常使用的成员。 请注意，默认情况下，如果第一个枚举成员的值未在声明中，设置其值为 0。

 如果有一个枚举<xref:System.FlagsAttribute>应用定义了零值的成员，其名称应为 None，以指示已在枚举中设置的任何值。 使用零值的成员的任何其他用途是违背使用<xref:System.FlagsAttribute>，AND 和 OR 按位运算符对该成员无用。 这意味着，只有一个成员应分配值为零。 请注意，如果具有多个成员值为零中将发生标志特性的枚举，`Enum.ToString()`返回不正确的结果不为零的成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复无标志特性枚举该规则的冲突，请定义一个具有值为零; 的成员这是一项非重大更改。 对于定义零值的成员的特性化标志枚举，None 将此成员，然后删除具有值为零; 的任何其他成员这是一项重大更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示除以前发布的特性标志化枚举此规则的警告。

## <a name="example"></a>示例
 下面的示例演示满足该规则的两个枚举和枚举， `BadTraceOptions`，这违反了该规则。

 [!code-cpp[FxCop.Design.EnumsZeroValue#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/cpp/FxCop.Design.EnumsZeroValue.cpp#1)]
 [!code-csharp[FxCop.Design.EnumsZeroValue#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/cs/FxCop.Design.EnumsZeroValue.cs#1)]
 [!code-vb[FxCop.Design.EnumsZeroValue#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/vb/FxCop.Design.EnumsZeroValue.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2217:不使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

 [CA1700:未命名的枚举值 Reserved](../code-quality/ca1700-do-not-name-enum-values-reserved.md)

 [CA1712:不要使用类型名称的枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

 [CA1028:枚举存储应为 Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

 [CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>请参阅
 <xref:System.Enum?displayProperty=fullName>
