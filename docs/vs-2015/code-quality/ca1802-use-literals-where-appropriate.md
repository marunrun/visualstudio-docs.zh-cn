---
title: CA1802：在适当的位置使用文本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseLiteralsWhereAppropriate
- CA1802
helpviewer_keywords:
- UseLiteralsWhereAppropriate
- CA1802
ms.assetid: 2515e4cd-9e61-486d-b067-58ba1a743ce4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dc8019c97d3c561000f1c6a8d083bee6253face3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544399"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802:在合适的位置使用文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 将在) 中 `static` 声明 `readonly` 和 `Shared` (`ReadOnly` 和 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ，并使用编译时可的值对字段进行初始化。

## <a name="rule-description"></a>规则描述
 `static``readonly`如果调用声明类型的静态构造函数，则将在运行时计算字段的值。 如果 `static``readonly` 字段在声明时被初始化并且静态构造函数不是显式声明的，则编译器将发出一个静态构造函数来初始化字段。

 字段的值 `const` 是在编译时计算的，并存储在元数据中，这会在与字段进行比较时增加运行时性能 `static``readonly` 。

 由于分配给目标字段的值是在编译时可的，因此将声明更改为 `const` 字段，以便在编译时而不是在运行时计算该值。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 `static` 和 `readonly` 修饰符替换为 `const` 修饰符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果性能不是问题，则可以安全地禁止显示此规则发出的警告，或禁用规则。

## <a name="example"></a>示例
 下面的示例演示了一个类型， `UseReadOnly` 该类型违反了规则和 `UseConstant` 满足规则的类型。

 [!code-csharp[FxCop.Performance.UseLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/cs/FxCop.Performance.UseLiterals.cs#1)]
 [!code-vb[FxCop.Performance.UseLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/vb/FxCop.Performance.UseLiterals.vb#1)]
