---
title: CA1502：避免过多的复杂性 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5da2e2bf26bb1894987caa8b748181d952bd7c18
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547831"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502:避免过度复杂
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AvoidExcessiveComplexity|
|CheckId|CA1502|
|类别|Microsoft 可维护性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法具有过多的圈复杂度。

## <a name="rule-description"></a>规则描述
 *圈复杂度* 通过方法测量线性独立路径的数量，该方法由条件分支的数量和复杂程度决定。 低圈复杂度通常表示一种易于理解、测试和维护的方法。 圈复杂度是通过方法的控制流图形计算得出的，其提供方式如下：

 圈复杂度 = 边数-节点数 + 1

 其中，节点表示逻辑分支点，边缘表示节点之间的线条。

 当圈复杂度大于25时，规则将报告冲突。

 可以在 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)中了解有关代码度量值的详细信息，

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请重构方法以降低其圈复杂度。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果复杂性无法轻易降低，并且方法易于理解、测试和维护，则可以安全地禁止显示此规则发出的警告。 特别是， `switch` 在) 语句中包含大型 (的方法 `Select` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 是排除的候选项。 在开发周期后期破坏代码的风险，或在以前发布的代码中引入运行时行为的意外更改可能超过重构代码的可维护性优势。

## <a name="how-cyclomatic-complexity-is-calculated"></a>如何计算圈复杂度
 圈复杂度的计算方法为：

-  (的分支数，例如 `if` 、 `while` 和 `do`) 

- 中的 `case` 语句数 `switch`

  下面的示例演示具有不同圈复杂度的方法。

## <a name="example"></a>示例
 **圈复杂度为1**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#1)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#1)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#1)]

## <a name="example"></a>示例
 **2的圈复杂度**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#2)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#2)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#2)]

## <a name="example"></a>示例
 **圈复杂度为3**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#3)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#3)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#3)]

## <a name="example"></a>示例
 **圈复杂度为8**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#4)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#4)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#4)]

## <a name="related-rules"></a>相关规则
 [CA1501:避免过度继承](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>另请参阅
 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
