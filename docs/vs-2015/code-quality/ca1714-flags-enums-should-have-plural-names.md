---
title: CA1714:枚举应采用复数形式的名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- FlagsEnumsShouldHavePluralNames
- CA1714
helpviewer_keywords:
- CA1714
- FlagsEnumsShouldHavePluralNames
ms.assetid: 95ef5b43-7681-49e9-a5a3-ac0357cf1be7
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bf0e75596bfc2b274f12d9b58d2718881931b7df
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700511"
---
# <a name="ca1714-flags-enums-should-have-plural-names"></a>CA1714:Flags 枚举应采用复数形式的名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|FlagsEnumsShouldHavePluralNames|
|CheckId|CA1714|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共枚举具有<xref:System.FlagsAttribute?displayProperty=fullName>和其名称不会结束中的。

## <a name="rule-description"></a>规则说明
 使用标记的类型<xref:System.FlagsAttribute>具有采用复数形式，因为该属性指示可以指定多个值的名称。 例如，枚举，用于定义每周天数可能被用于应用程序中您可以在其中指定多天。 此枚举应具有<xref:System.FlagsAttribute>且无法调用天。 允许仅指定一天的类似枚举将没有属性，并可能是名为 Day。

 命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。

## <a name="how-to-fix-violations"></a>如何解决冲突
 确保枚举名称的复数形式的单词，或删除<xref:System.FlagsAttribute>属性如果不应同时指定多个枚举值。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 则可以安全地禁止显示冲突，如果名称为复数形式的单词，但不是以结尾的。 例如，如果所述的多个天枚举以前名为 DaysOfTheWeek，这会违反该规则，但不是其意图的逻辑。 此类违规情况应禁止显示。

## <a name="related-rules"></a>相关的规则
 [CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217:不使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>请参阅
 <xref:System.FlagsAttribute?displayProperty=fullName> [枚举设计](https://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)
