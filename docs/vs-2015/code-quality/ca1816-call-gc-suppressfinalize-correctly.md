---
title: CA1816：调用 GC。Gc.suppressfinalize 正确 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1816
- DisposeMethodsShouldCallSuppressFinalize
helpviewer_keywords:
- DisposeMethodsShouldCallSuppressFinalize
- CA1816
ms.assetid: 47915fbb-103f-4333-b157-1da16bf49660
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 532478a8d6ed6b88347d196b4a74b6f19a38ef85
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546765"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816:正确调用 GC.SuppressFinalize
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|Category|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

- 作为实现的方法 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 不会调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

- 不是调用的实现的方法 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

- 方法调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 并传递除此外的其他内容（我在 Visual Basic 中）。

## <a name="rule-description"></a>规则描述
 使用 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 方法，用户可以在对象变为垃圾回收之前随时释放资源。 如果 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 调用方法，它将释放对象的资源。 这使得不需要终止。 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>应调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> ，以便垃圾回收器不会调用该对象的终结器。

 若要防止具有终结器的派生类型必须重新实现 [IDisposable] （<!-- TODO: review code entity reference <xref:assetId:///System.IDisposable?qualifyHint=True&amp;autoUpgrade=False>  -->）并调用它时，无需终结器的非密封类型仍应调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请执行以下操作：

 如果该方法是的实现 <xref:System.IDisposable.Dispose%2A> ，则添加对的调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

 如果该方法不是的实现 <xref:System.IDisposable.Dispose%2A> ，则删除对的调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 或将其移动到该类型的 <xref:System.IDisposable.Dispose%2A> 实现。

 更改对的所有调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 以传递此项（在 Visual Basic 中为 Me）。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当 deliberating 使用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 来控制其他对象的生存期时，才禁止显示此规则发出的警告。 如果的实现不调用，请不要禁止显示此规则发出的警告 <xref:System.IDisposable.Dispose%2A> <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。 在这种情况下，无法取消终止会降低性能，而且不会带来任何好处。

## <a name="example"></a>示例
 下面的示例演示错误调用的方法 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly.vb#1)]

## <a name="example"></a>示例
 下面的示例演示正确调用的方法 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2215:Dispose 方法应调用基类释放](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA2216:可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>另请参阅
 [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
