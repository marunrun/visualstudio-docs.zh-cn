---
title: CA1816:正确调用 GC.SuppressFinalize
ms.date: 06/30/2018
ms.topic: reference
f1_keywords:
- CA1816
- DisposeMethodsShouldCallSuppressFinalize
helpviewer_keywords:
- DisposeMethodsShouldCallSuppressFinalize
- CA1816
ms.assetid: 47915fbb-103f-4333-b157-1da16bf49660
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2c14f9ed8803c02d1570ac2a3dee82fbdfca5f01
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62796775"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816:正确调用 GC.SuppressFinalize

|||
|-|-|
|TypeName|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|类别|Microsoft。 用法|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

此规则冲突的情况导致的：

- 是的实现的方法<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>并不会调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>。

- 不是一种实现的方法<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>并调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>。

- 调用的方法<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>并不是传递[此 (C#)](/dotnet/csharp/language-reference/keywords/this)或[我 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)。

## <a name="rule-description"></a>规则说明

<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>方法可让用户随时可用于垃圾回收的对象之前释放资源。 如果<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>方法调用时，它释放的对象的资源。 这使得无需终止。 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 应调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>使垃圾回收器不会调用对象的终结器。

若要防止派生的类型有终结器无需重新实现<xref:System.IDisposable>并调用它，未密封的类型而无需终结器仍应调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突：

- 如果此方法的实现<xref:System.IDisposable.Dispose%2A>，添加对的调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>。

- 如果此方法不是实现<xref:System.IDisposable.Dispose%2A>，请删除对<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>或将其移到该类型的<xref:System.IDisposable.Dispose%2A>实现。

- 更改所有调用的<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>传递[此 (C#)](/dotnet/csharp/language-reference/keywords/this)或[我 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果有意使用仅禁止显示此规则的警告<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>来控制其他对象的生存期。 如果的实现不禁止显示此规则的警告<xref:System.IDisposable.Dispose%2A>不会调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>。 在此情况下，无法取消终止操作会降低性能，未提供任何好处。

## <a name="example-that-violates-ca1816"></a>违反了 CA1816 的示例

此代码显示了调用的方法<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>，但不满足[此 (C#)](/dotnet/csharp/language-reference/keywords/this)或[我 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)。 因此，此代码违反规则 CA1816。

[!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../code-quality/codesnippet/VisualBasic/ca1816-call-gc-suppressfinalize-correctly_1.vb)]
[!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../code-quality/codesnippet/CSharp/ca1816-call-gc-suppressfinalize-correctly_1.cs)]

## <a name="example-that-satisfies-ca1816"></a>满足 CA1816 的示例

此示例显示了一种方法的正确调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>通过传递[此 (C#)](/dotnet/csharp/language-reference/keywords/this)或[我 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)。

[!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../code-quality/codesnippet/VisualBasic/ca1816-call-gc-suppressfinalize-correctly_2.vb)]
[!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../code-quality/codesnippet/CSharp/ca1816-call-gc-suppressfinalize-correctly_2.cs)]

## <a name="related-rules"></a>相关的规则

- [CA2215:方法应调用基类 dispose](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)
- [CA2216:可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>请参阅

- [释放模式](/dotnet/standard/design-guidelines/dispose-pattern)