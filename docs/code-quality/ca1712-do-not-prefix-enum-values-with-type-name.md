---
title: CA1712：不要将类型名用作枚举值的前缀
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1712
- DoNotPrefixEnumValuesWithTypeName
helpviewer_keywords:
- CA1712
- DoNotPrefixEnumValuesWithTypeName
ms.assetid: df0e3a12-67bf-48f1-a10b-2ef60484a5c7
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: f151296fce00ca92209c588c4be0361f9adfc7fd
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72348939"
---
# <a name="ca1712-do-not-prefix-enum-values-with-type-name"></a>CA1712：不要将类型名用作枚举值的前缀

|||
|-|-|
|TypeName|DoNotPrefixEnumValuesWithTypeName|
|CheckId|CA1712|
|类别|Microsoft。命名|
|重大更改|重大|

## <a name="cause"></a>原因
枚举包含名称以枚举的类型名称开头的成员。

## <a name="rule-description"></a>规则说明
枚举成员的名称不带有类型名称前缀，因为开发工具应提供类型信息。

命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了了解新的软件库所需的时间，并使客户对库的开发更加自信，因为有开发托管代码的专业技能。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请从枚举成员中删除类型名称前缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示一个错误命名枚举，后跟更正后的版本。

[!code-csharp[FxCop.Naming.EnumValues#1](../code-quality/codesnippet/CSharp/ca1712-do-not-prefix-enum-values-with-type-name_1.cs)]
[!code-cpp[FxCop.Naming.EnumValues#1](../code-quality/codesnippet/CPP/ca1712-do-not-prefix-enum-values-with-type-name_1.cpp)]
[!code-vb[FxCop.Naming.EnumValues#1](../code-quality/codesnippet/VisualBasic/ca1712-do-not-prefix-enum-values-with-type-name_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1711：标识符应采用正确的后缀](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

[CA1027：用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

[CA2217：不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217.md)

## <a name="see-also"></a>请参阅

- <xref:System.Enum?displayProperty=fullName>