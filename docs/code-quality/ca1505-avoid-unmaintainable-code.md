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
ms.openlocfilehash: 740ef26af6f1f84d23ef27de5176df1b3de98b34
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62797319"
---
# <a name="ca1505-avoid-unmaintainable-code"></a>CA1505:避免使用无法维护的代码

|||
|-|-|
|TypeName|AvoidUnmantainableCode|
|CheckId|CA1505|
|类别|Microsoft.Maintainability|
|是否重大更改|非换行|

## <a name="cause"></a>原因

类型或方法具有较低的可维护性索引值。

## <a name="rule-description"></a>规则说明

通过使用以下度量值计算的可维护性索引： 行代码，程序卷和圈复杂度。 程序卷是了解类型或方法的运算符和操作数在代码中的数量为基础的难易程度的度量值。 圈复杂度是复杂性的度量值的类型或方法的结构化。 您可以了解有关代码的指标的详细信息[测量复杂性和可维护性托管代码的](../code-quality/code-metrics-values.md)。

较低的可维护性索引指示类型或方法可能难以维护而且可能会重新设计的良好候选项。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此冲突，重新设计的类型或方法，并尝试将其拆分为较小且更集中的类型或方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

在类型或方法不能拆分或被视为可维护性，尽管其尺寸大时，可以禁止显示此警告。

## <a name="see-also"></a>请参阅

- [可维护性警告](../code-quality/maintainability-warnings.md)
- [测量托管代码的复杂性和可维护性](../code-quality/code-metrics-values.md)