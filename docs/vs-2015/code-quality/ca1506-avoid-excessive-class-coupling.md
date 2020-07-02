---
title: CA1506：避免过多的类耦合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveClassCoupling
- CA1506
helpviewer_keywords:
- AvoidExcessiveClassCoupling
- CA1506
ms.assetid: 9f0943c0-e802-4e3f-8798-2ab8653ddc80
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 07f19cb9d4aa2ed118898a1816092479cbd16565
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545699"
---
# <a name="ca1506-avoid-excessive-class-coupling"></a>CA1506:避免过度类耦合度
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AvoidExcessiveClassCoupling|
|CheckId|CA1506|
|类别|Microsoft 可维护性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型或方法与许多其他类型耦合在一起。

## <a name="rule-description"></a>规则描述
 此规则通过计算类型或方法包含的唯一类型引用的个数来衡量类耦合。

 类耦合度较高的类型和方法可能很难维护。 有一种很好的做法，就是使用表现低耦合和高聚合的类型和方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此冲突，请尝试重新设计类型或方法，以减少其耦合的类型的数量。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果类型或方法仍被视为可维护（尽管它对其他类型的依赖项很多），则排除此警告。

## <a name="see-also"></a>另请参阅
 [测量托管代码的复杂性和可维护性的](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)可[维护性警告](../code-quality/maintainability-warnings.md)
