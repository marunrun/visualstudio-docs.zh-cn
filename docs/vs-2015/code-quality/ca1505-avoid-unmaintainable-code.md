---
title: CA1505：避免编写无法维护代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnmaintainableCode
- CA1505
helpviewer_keywords:
- AvoidUnmaintainableCode
- CA1505
ms.assetid: 8292b268-5929-4221-b699-f9c414bcec5d
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 87aacfd675181e35d289b2a054c58f83f3f790fa
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72607592"
---
# <a name="ca1505-avoid-unmaintainable-code"></a>CA1505：避免编写无法维护的代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidUnmantainableCode|
|CheckId|CA1505|
|类别|Microsoft 可维护性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型或方法具有较低的可维护性索引值。

## <a name="rule-description"></a>规则说明
 可维护性索引使用以下度量值进行计算：代码行、程序量和圈复杂度。 "程序卷" 是对基于代码中的运算符和操作数的数量进行理解的难度。 圈复杂度是指类型或方法的结构复杂度的度量。 可以在[测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)中了解有关代码度量值的详细信息。

 低可维护性索引指示类型或方法可能难以维护，并且是重新设计的良好候选项。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此冲突，请重新设计类型或方法，并尝试将其拆分为更小且更有针对性的类型或方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 当类型或方法仍被视为可维护（尽管其大小大或者无法拆分类型或方法时）时，请排除此警告。

## <a name="see-also"></a>请参阅
 [测量托管代码的复杂性和可维护性的](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)可[维护性警告](../code-quality/maintainability-warnings.md)
