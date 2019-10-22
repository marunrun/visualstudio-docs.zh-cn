---
title: CA2213：应释放可释放的字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DisposableFieldsShouldBeDisposed
- CA2213
helpviewer_keywords:
- CA2213
- DisposableFieldsShouldBeDisposed
ms.assetid: e99442c9-70e2-47f3-b61a-d8ac003bc6e5
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8ebeae3e5e367bb2c1a09bc1cb38dcc80d2c3826
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662900"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213：应释放可释放的字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 实现 <xref:System.IDisposable?displayProperty=fullName> 声明类型的字段，这些字段也实现 <xref:System.IDisposable>。 该字段的 <xref:System.IDisposable.Dispose%2A> 方法不由声明类型的 <xref:System.IDisposable.Dispose%2A> 方法调用。

## <a name="rule-description"></a>规则说明
 类型负责释放其所有非托管资源;这是通过实现 <xref:System.IDisposable> 来完成的。 此规则检查是否有可释放类型 `T` 声明 `F` 为可释放类型 `FT` 实例的字段。 对于 `F` 的每个字段，该规则将尝试查找对 `FT.Dispose` 的调用。 此规则将搜索 `T.Dispose` 调用的方法，一个级别较低（由 `FT.Dispose` 调用的方法调用的方法）。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请对具有实现 <xref:System.IDisposable> 的类型的字段调用 <xref:System.IDisposable.Dispose%2A> （如果你负责分配和释放字段所持有的非托管资源）。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果你不负责释放字段持有的资源，或者如果对 <xref:System.IDisposable.Dispose%2A> 的调用发生在比规则检查更深的调用级别上，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示实现 <xref:System.IDisposable> 的类型 `TypeA` （上一讨论中的 `FT`）。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>示例
 下面的示例演示了一个类型 `TypeB`，该类型违反此规则，方法是将字段 `aFieldOfADisposableType` （在上一讨论中 `F`）声明为可释放的类型（`TypeA`），而不是对字段调用 <xref:System.IDisposable.Dispose%2A>。 `TypeB` 对应于前面讨论的 `T`。

 [!code-csharp[FxCop.Usage.IDisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableFields/cs/FxCop.Usage.IDisposableFields.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.IDisposable?displayProperty=fullName> [Dispose 模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
