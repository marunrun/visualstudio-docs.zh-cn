---
title: CA1802:在适用处使用原义字符 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5990d8ea3720098651d3ed696f6ee5ff907b82f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143147"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802:在合适的位置使用文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 字段声明`static`并`readonly`(`Shared`并`ReadOnly`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)])，并使用在编译时计算的值初始化。

## <a name="rule-description"></a>规则说明
 值`static``readonly`时调用的声明类型的静态构造函数，在运行时将计算字段。 如果`static``readonly`字段会初始化时它声明和静态构造函数未显式声明，则编译器将发出静态构造函数来初始化该字段。

 值`const`字段是在编译时计算和存储在元数据，这会增加运行时性能相比到`static``readonly`字段。

 因为分配给目标字段的值可在编译时，将声明更改为`const`字段，以便在编译时而不是在运行时计算的值。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，替换`static`并`readonly`修饰符用于`const`修饰符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果无需关注性能，它是安全地禁止显示此规则的警告或禁用规则。

## <a name="example"></a>示例
 下面的示例演示一种类型， `UseReadOnly`，这违反了规则和一个类型， `UseConstant`，满足该规则。

 [!code-csharp[FxCop.Performance.UseLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/cs/FxCop.Performance.UseLiterals.cs#1)]
 [!code-vb[FxCop.Performance.UseLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/vb/FxCop.Performance.UseLiterals.vb#1)]
