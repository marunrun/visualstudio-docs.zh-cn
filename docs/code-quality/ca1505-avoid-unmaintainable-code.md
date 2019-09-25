---
title: CA1505:避免使用无法维护的代码
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidUnmaintainableCode
- CA1505
helpviewer_keywords:
- AvoidUnmaintainableCode
- CA1505
ms.assetid: 8292b268-5929-4221-b699-f9c414bcec5d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3ba027ef2e663870d0af50bc6d2154133f7980c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234546"
---
# <a name="ca1505-avoid-unmaintainable-code"></a>CA1505:避免使用无法维护的代码

|||
|-|-|
|TypeName|AvoidUnmantainableCode|
|CheckId|CA1505|
|类别|Microsoft.Maintainability|
|重大更改|不间断|

## <a name="cause"></a>原因

类型或方法具有较低的可维护性索引值。

## <a name="rule-description"></a>规则说明

可维护性索引使用以下度量值进行计算：代码行、程序量和圈复杂度。 程序卷是对基于代码中的运算符和操作数的数目了解类型或方法有难度的度量。 圈复杂度是指类型或方法的结构复杂度的度量。 可以在[测量托管代码的复杂性和可维护性](../code-quality/code-metrics-values.md)中了解有关代码度量值的详细信息。

低可维护性索引指示类型或方法可能难以维护，并且是重新设计的良好候选项。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此冲突，请重新设计类型或方法，并尝试将其拆分为更小且更有针对性的类型或方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果类型或方法不能拆分或被视为可维护（尽管其大小很大），可以禁止显示此警告。

## <a name="see-also"></a>请参阅

- [可维护性警告](../code-quality/maintainability-warnings.md)
- [测量托管代码的复杂性和可维护性](../code-quality/code-metrics-values.md)