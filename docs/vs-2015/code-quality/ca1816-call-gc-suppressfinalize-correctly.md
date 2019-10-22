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
ms.openlocfilehash: acc86c278faa877897d294e72632762eff834a76
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668389"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816：正确调用 GC.SuppressFinalize
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|类别|微软. 用法|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

- 作为 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 的实现的方法不调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>。

- 不是 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 的实现的方法。

- 方法调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>，并传递除此外的其他内容（我在 Visual Basic 中）。

## <a name="rule-description"></a>规则说明
 使用 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 方法，用户可以在对象变为垃圾回收之前随时释放资源。 如果调用 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 方法，则它将释放对象的资源。 这使得不需要终止。 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 应调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>，因此垃圾回收器不会调用该对象的终结器。

 若要防止具有终结器的派生类型必须重新实现 [IDisposable] （<!-- TODO: review code entity reference <xref:assetId:///System.IDisposable?qualifyHint=True&amp;autoUpgrade=False>  -->）并调用它，不带终结器的非密封类型仍应调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请执行以下操作：

 如果该方法是 <xref:System.IDisposable.Dispose%2A> 的实现，请添加对 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 的调用。

 如果该方法不是 <xref:System.IDisposable.Dispose%2A> 的实现，则删除对 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 的调用或将其移动到类型的 <xref:System.IDisposable.Dispose%2A> 实现中。

 更改所有对 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 的调用以传递此项（Visual Basic 中的）。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当 deliberating 使用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 控制其他对象的生存期时，才禁止显示此规则发出的警告。 如果 <xref:System.IDisposable.Dispose%2A> 的实现没有调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>，请不要禁止显示此规则发出的警告。 在这种情况下，无法取消终止会降低性能，而且不会带来任何好处。

## <a name="example"></a>示例
 下面的示例演示了一个不正确地调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 的方法。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly.vb#1)]

## <a name="example"></a>示例
 下面的示例演示了一个正确调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 的方法。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2215：Dispose 方法应调用基类 Dispose](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA2216：可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>请参阅
 [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
