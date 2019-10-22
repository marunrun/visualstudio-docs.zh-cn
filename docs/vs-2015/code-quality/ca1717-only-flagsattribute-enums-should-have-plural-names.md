---
title: CA1717：仅 FlagsAttribute 枚举应包含复数名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1717
- OnlyFlagsEnumsShouldHavePluralNames
helpviewer_keywords:
- OnlyFlagsEnumsShouldHavePluralNames
- CA1717
ms.assetid: a6855d8b-d78a-42c1-834e-61c31f5572ed
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0c378d419be0d964c27cfcbe523fbe3a33da97b8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669086"
---
# <a name="ca1717-only-flagsattribute-enums-should-have-plural-names"></a>CA1717：只有 FlagsAttribute 枚举应采用复数形式的名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OnlyFlagsEnumsShouldHavePluralNames|
|CheckId|CA1717|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见枚举的名称以复数形式结束，并且未使用 <xref:System.FlagsAttribute?displayProperty=fullName> 特性标记枚举。

## <a name="rule-description"></a>规则说明
 命名约定规定，复数名称的枚举指示可以同时指定多个枚举值。 @No__t_0 告诉编译器，应将枚举视为对枚举启用按位运算的位域。

 如果一次只能指定一个枚举值，则枚举的名称应为单数形式的单词。 例如，定义一周中各天的枚举可能适用于可指定多天的应用程序。 此枚举应具有 <xref:System.FlagsAttribute>，并且可以称为 "Days"。 只允许指定一天的类似枚举不具有属性，并且可以称为 "Day"。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了学习新软件库所需的时间，并使客户对库的开发更加自信，因为有开发托管代码的专业技能。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将枚举的名称设置为单数字，或添加 <xref:System.FlagsAttribute>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果名称以单数形式出现，则可以安全地禁止显示规则。

## <a name="related-rules"></a>相关规则
 [CA1714：Flags 枚举应采用复数形式的名称](../code-quality/ca1714-flags-enums-should-have-plural-names.md)

 [CA1027：用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217：不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>请参阅
 <xref:System.FlagsAttribute?displayProperty=fullName>[枚举设计](https://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)
