---
title: CA1027:用 FlagsAttribute 标记枚举 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkEnumsWithFlags
- CA1027
helpviewer_keywords:
- CA1027
- MarkEnumsWithFlags
ms.assetid: 249e882c-8cd1-4c00-a2de-7b6bdc1849ff
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6603e0869a9eb7947735c52a4c438b39d64b9140
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157716"
---
# <a name="ca1027-mark-enums-with-flagsattribute"></a>CA1027:用 FlagsAttribute 标记枚举
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkEnumsWithFlags|
|CheckId|CA1027|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共枚举的值为 2 的幂或是在枚举中定义其他值的组合和<xref:System.FlagsAttribute?displayProperty=fullName>属性不存在。 若要减少误报，此规则不会报告具有连续值的枚举冲突。

## <a name="rule-description"></a>规则说明
 枚举是一种值类型，它定义一组相关的已命名常数。 将应用<xref:System.FlagsAttribute>到枚举时可以有意义的方式组合已命名的常数。 例如，考虑应用程序，用于跟踪提供了哪一天的资源中星期几的枚举。 如果通过使用枚举具有编码的每个资源可用性<xref:System.FlagsAttribute>可以表示存在，天内的任意组合。 如果没有属性，可以表示只有一个日期是星期几。

 对于存储可组合枚举的字段，单独的枚举值被视为位字段中的组。 因此，此类字段有时称为*位域*。 若要组合的枚举值的位域中的存储，使用布尔条件运算符。 若要测试以确定是否存在特定的枚举值的位字段，请使用布尔逻辑运算符。 对于存储和检索正确组合的枚举值的位字段，每个枚举中定义的值必须是 2 的幂。 除非该条件，否则布尔逻辑运算符不能提取字段中存储的单独的枚举值。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请添加<xref:System.FlagsAttribute>到枚举。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果不希望可组合的枚举值，禁止显示此规则的警告。

## <a name="example"></a>示例
 在以下示例中，`DaysEnumNeedsFlags`是满足的要求使用一个枚举<xref:System.FlagsAttribute>，但不是希望其。 `ColorEnumShouldNotHaveFlag`枚举不具有值 2 的幂，但未正确指定<xref:System.FlagsAttribute>。 这违反了规则[CA2217:执行不使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)。

 [!code-csharp[FxCop.Design.EnumFlags#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumFlags/cs/FxCop.Design.EnumFlags.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA2217:不使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>请参阅
 <xref:System.FlagsAttribute?displayProperty=fullName>
