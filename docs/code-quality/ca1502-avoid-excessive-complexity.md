---
title: CA1502:避免过度复杂
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidExcessiveComplexity
- CA1502
helpviewer_keywords:
- CA1502
- AvoidExcessiveComplexity
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: e968cef6491e1c24d98e5f64248b5104db8c5b65
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62797403"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502:避免过度复杂

|||
|-|-|
|TypeName|AvoidExcessiveComplexity|
|CheckId|CA1502|
|类别|Microsoft.Maintainability|
|是否重大更改|非换行|

## <a name="cause"></a>原因

一种方法具有过多的圈复杂度。

## <a name="rule-description"></a>规则说明

*圈复杂度*测量线性独立的方法，由数量和复杂程度的条件分支路径的数量。 低圈复杂度通常指示很容易理解、 测试和维护的方法。 圈复杂度计算方法的控制流关系图中，按如下所示计算公式：

圈复杂度 = 边缘的节点数 + 1 的数

一个*节点*表示逻辑分支点和一个*边缘*表示节点之间的直线。

超过 25 种的圈复杂度时，规则将报告冲突。

您可以了解有关代码的指标的详细信息[测量托管代码的复杂性](../code-quality/code-metrics-values.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请重构的方法，以减少其圈复杂度。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果不能轻松地降低复杂程度，并且该方法很容易理解、 测试和维护。 具体而言，包含较大的方法`switch`(`Select`中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) 语句可用于排除。 破坏代码库后期在开发周期或以前发布的代码中的运行时行为中发生意外变化可能会得不偿失可维护性的重构代码的风险。

## <a name="how-cyclomatic-complexity-is-calculated"></a>如何计算圈复杂度

圈复杂度计算通过将 1 添加到以下：

- 分支数 (如`if`， `while`，和`do`)

- 数`case`中的语句 `switch`

## <a name="example"></a>示例

以下示例显示圈复杂度不断变化的方法。

**为 1 的圈复杂度**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_1.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_1.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_1.cs)]

## <a name="example"></a>示例

**圈复杂度为 2**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_2.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_2.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_2.cs)]

## <a name="example"></a>示例

**圈复杂度为 3**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_3.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_3.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_3.cs)]

## <a name="example"></a>示例

**圈复杂度为 8**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_4.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_4.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_4.cs)]

## <a name="related-rules"></a>相关的规则

[CA1501:避免过度继承](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>请参阅

- [测量托管代码的复杂性和可维护性](../code-quality/code-metrics-values.md)