---
title: CA1506:避免过度类耦合度
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidExcessiveClassCoupling
- CA1506
helpviewer_keywords:
- AvoidExcessiveClassCoupling
- CA1506
ms.assetid: 9f0943c0-e802-4e3f-8798-2ab8653ddc80
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b655609548d3de293abe2adc0ec3fb5c6fcf297b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546103"
---
# <a name="ca1506-avoid-excessive-class-coupling"></a>CA1506:避免过度类耦合度

|||
|-|-|
|TypeName|AvoidExcessiveClassCoupling|
|CheckId|CA1506|
|类别|Microsoft.Maintainability|
|是否重大更改|重大|

## <a name="cause"></a>原因

与许多其他类型结合使用的类型或方法。

## <a name="rule-description"></a>规则说明

此规则通过计算类型或方法包含的唯一类型引用的个数来衡量类耦合。

具有类耦合度很高的类型和方法可能很难维护。 最好能够表现出低耦合和高聚合的类型和方法。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此冲突，请尝试重新设计的类型或方法来减少之耦合的类型的数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果类型或方法被视为可维护性，尽管其大量的其他类型的依赖项，请排除此警告。

## <a name="see-also"></a>请参阅

- [维护性警告](../code-quality/maintainability-warnings.md)
- [测量托管代码的复杂性和可维护性](../code-quality/code-metrics-values.md)