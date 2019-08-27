---
title: CA1502:避免过度复杂 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveComplexity
- CA1502
helpviewer_keywords:
- CA1502
- AvoidExcessiveComplexity
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e1885a07f4c9edbbdea9be4f0e74aaf8e4d3a6f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191258"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502:避免过度复杂
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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

 其中一个节点表示逻辑分支点，边缘表示节点之间的直线。

 超过 25 种的圈复杂度时，规则将报告冲突。

 您可以了解有关代码的指标的详细信息[测量复杂性和托管代码可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)，

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请重构的方法，以减少其圈复杂度。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果不能轻松地降低复杂程度，并且该方法很容易理解、 测试和维护。 具体而言，包含较大的方法`switch`(`Select`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 语句可用于排除。 破坏代码库后期在开发周期或以前发布的代码中的运行时行为中发生意外变化可能会得不偿失可维护性的重构代码的风险。

## <a name="how-cyclomatic-complexity-is-calculated"></a>如何计算圈复杂度
 圈复杂度计算通过将 1 添加到以下：

- 分支数 (如`if`， `while`，和`do`)

- 数`case`中的语句 `switch`

  以下示例显示圈复杂度不断变化的方法。

## <a name="example"></a>示例
 **为 1 的圈复杂度**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#1)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#1)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#1)]

## <a name="example"></a>示例
 **圈复杂度为 2**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#2)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#2)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#2)]

## <a name="example"></a>示例
 **圈复杂度为 3**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#3)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#3)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#3)]

## <a name="example"></a>示例
 **圈复杂度为 8**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#4)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#4)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#4)]

## <a name="related-rules"></a>相关的规则
 [CA1501:避免过度继承](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>请参阅
 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
