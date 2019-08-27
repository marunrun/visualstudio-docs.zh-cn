---
title: CA1821:移除空终结器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveEmptyFinalizers
- CA1821
helpviewer_keywords:
- CA1821
ms.assetid: 3f4855a0-e4a0-46e6-923c-4c3b7074048d
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5a6175871e74bf3cb99610dce0926f0982f331d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201668"
---
# <a name="ca1821-remove-empty-finalizers"></a>CA1821:移除空终结器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|RemoveEmptyFinalizers|
|CheckId|CA1821|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 一个类型实现终结器为空、 调用仅基类型终结器，或只按条件发出的方法调用。

## <a name="rule-description"></a>规则说明
 应尽可能避免终结器，因为跟踪对象生存期会产生额外的性能系统开销。 它收集对象前，垃圾回收器将运行终结器。 这意味着两个集合需要回收该对象。 空终结器会产生此增加的开销毫无益处。

## <a name="how-to-fix-violations"></a>如何解决冲突
 移除空终结器。 如果终结器才可进行调试，则将在整个终结器`#if DEBUG / #endif`指令。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示此规则的消息。 取消终止失败会降低性能，并不提供任何好处。

## <a name="example"></a>示例
 下面的示例显示了应移除空终结器、 终结器应括起来的`#if DEBUG / #endif`指令和使用终结器`#if DEBUG / #endif`指令正确。

 [!code-csharp[FxCop.Performance.RemoveEmptyFinalizers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RemoveEmptyFinalizers/cs/FxCop.Performance.RemoveEmptyFinalizers.cs#1)]
