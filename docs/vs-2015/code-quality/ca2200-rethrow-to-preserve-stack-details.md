---
title: CA2200:重新引发以保留堆栈详细信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RethrowToPreserveStackDetails
- CA2200
helpviewer_keywords:
- CA2200
- RethrowToPreserveStackDetails
ms.assetid: 046e1b98-c4dc-4515-874f-9c0de2285621
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ed2dd2884268511ae05ac89c132f73fdf8b2771e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201645"
---
# <a name="ca2200-rethrow-to-preserve-stack-details"></a>CA2200:再次引发以保留堆栈详细信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|RethrowToPreserveStackDetails|
|CheckId|CA2200|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 将重新引发异常，，和中显式指定的异常`throw`语句。

## <a name="rule-description"></a>规则说明
 一旦引发异常，它携带的一部分是信息的堆栈跟踪。 堆栈跟踪是开头的方法引发的异常和结束的捕获的异常的方法的方法调用层次结构的列表。 如果通过指定在异常重新引发异常`throw`语句在当前方法中重新启动的堆栈跟踪和引发异常的原始方法与当前方法之间的方法调用列表将丢失。 若要保持与异常的原始堆栈跟踪信息，请使用`throw`而无需指定异常的语句。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，重新而无需显式指定异常引发的异常。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一种方法， `CatchAndRethrowExplicitly`，这违反了规则和方法， `CatchAndRethrowImplicitly`，以及满足该规则。

 [!code-csharp[FxCop.Usage.Rethrow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/cs/FxCop.Usage.Rethrow.cs#1)]
 [!code-vb[FxCop.Usage.Rethrow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/vb/FxCop.Usage.Rethrow.vb#1)]
