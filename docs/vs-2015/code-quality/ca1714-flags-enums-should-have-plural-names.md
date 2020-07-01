---
title: CA1714：标志枚举应包含复数名称 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 74e93a9644f365120117bd247d2ea8b9d43608cb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548182"
---
# <a name="ca1714-flags-enums-should-have-plural-names"></a>CA1714:Flags 枚举应采用复数形式的名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|FlagsEnumsShouldHavePluralNames|
|CheckId|CA1714|
|Category|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共枚举具有 <xref:System.FlagsAttribute?displayProperty=fullName> ，且其名称不以 "" 结尾。

## <a name="rule-description"></a>规则描述
 标记有的类型 <xref:System.FlagsAttribute> 具有复数形式的名称，因为该特性指示可以指定多个值。 例如，定义一周中各天的枚举可能适用于可指定多天的应用程序。 此枚举应具有 <xref:System.FlagsAttribute> ，并且可以称为 "Days"。 只允许指定一天的类似枚举不具有属性，并且可以称为 "Day"。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将枚举的名称设置为复数字， <xref:System.FlagsAttribute> 如果不应同时指定多个枚举值，则删除该属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果名称是复数形式的单词，但不是以 "" 结尾，则可以安全地禁止显示冲突。 例如，如果前面介绍的多天枚举名为 "DaysOfTheWeek"，则这将违反规则的逻辑，而不是其意图。 此类冲突应为 suppressd。

## <a name="related-rules"></a>相关规则
 [CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217:不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>另请参阅
 <xref:System.FlagsAttribute?displayProperty=fullName>[枚举设计](https://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)
