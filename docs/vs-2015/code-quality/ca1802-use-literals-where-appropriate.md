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
ms.openlocfilehash: bbcf83772a7a4031cf2e27abe7e8f4c08e21c11c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671516"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802：在合适的位置使用文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 @No__t_0 和 `readonly` （在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中 `Shared` 和 `ReadOnly`）声明字段，并使用编译时可的值初始化。

## <a name="rule-description"></a>规则说明
 如果调用声明类型的静态构造函数，则在运行时计算 `static``readonly` 字段的值。 如果 `static``readonly` 字段在声明时进行了初始化并且静态构造函数不是显式声明的，则编译器将发出一个静态构造函数来初始化字段。

 在编译时计算 `const` 字段的值，并将其存储在元数据中，这会在与 `static``readonly` 字段进行比较时增加运行时性能。

 由于分配给目标字段的值是在编译时可的，因此将声明更改为 `const` 字段，以便在编译时而不是在运行时计算该值。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用 `const` 修饰符替换 `static` 和 `readonly` 修饰符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果性能不是问题，则可以安全地禁止显示此规则发出的警告，或禁用规则。

## <a name="example"></a>示例
 下面的示例演示了违反规则的类型 `UseReadOnly`，以及满足规则的类型 `UseConstant`。

 [!code-csharp[FxCop.Performance.UseLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/cs/FxCop.Performance.UseLiterals.cs#1)]
 [!code-vb[FxCop.Performance.UseLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/vb/FxCop.Performance.UseLiterals.vb#1)]
