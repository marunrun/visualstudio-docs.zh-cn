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
ms.openlocfilehash: 3fdd20df37586e50b5236872f1d84de48d08c87a
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233528"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816:正确调用 GC.SuppressFinalize

|||
|-|-|
|TypeName|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|类别|微软. 用法|
|重大更改|不间断|

## <a name="cause"></a>原因

此规则的冲突可能由以下原因引起：

- 一个方法，它是的<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>实现，不会调用。 <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>

- 不是的<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>实现并调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>的方法。

- 调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>并传递除[此C#（）](/dotnet/csharp/language-reference/keywords/this)或[Me （Visual Basic）](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)以外的其他内容的方法。

## <a name="rule-description"></a>规则说明

使用<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>方法，用户可以在对象变为垃圾回收之前随时释放资源。 如果调用<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>方法，它将释放对象的资源。 这使得不需要终止。 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>应调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> ，以便垃圾回收器不会调用该对象的终结器。

若要防止具有终结器的派生类型必须<xref:System.IDisposable>重新实现并调用它，则不需要终结器的<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>非密封类型仍应调用。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请执行以下操作：

- 如果该方法是的<xref:System.IDisposable.Dispose%2A>实现，则添加对<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>的调用。

- 如果该方法不是的<xref:System.IDisposable.Dispose%2A>实现，则删除对<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>的调用或将其移动到该类型的<xref:System.IDisposable.Dispose%2A>实现。

- 更改对<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>的所有调用以传递[此C#（）](/dotnet/csharp/language-reference/keywords/this)或[Me （Visual Basic）](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当有意使用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>控制其他对象的生存期时，才禁止显示此规则发出的警告。 如果的<xref:System.IDisposable.Dispose%2A>实现不调用<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>，请不要禁止显示此规则发出的警告。 在这种情况下，无法取消终止会降低性能，而且不会带来任何好处。

## <a name="example-that-violates-ca1816"></a>违反 CA1816 的示例

此代码显示一个方法，该<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>方法调用，但不传递[C#（）](/dotnet/csharp/language-reference/keywords/this)或[Me （Visual Basic）](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)。 因此，此代码违反了规则 CA1816。

[!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../code-quality/codesnippet/VisualBasic/ca1816-call-gc-suppressfinalize-correctly_1.vb)]
[!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../code-quality/codesnippet/CSharp/ca1816-call-gc-suppressfinalize-correctly_1.cs)]

## <a name="example-that-satisfies-ca1816"></a>满足 CA1816 的示例

此示例演示通过传递<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> [此（C#）](/dotnet/csharp/language-reference/keywords/this)或[Me （Visual Basic）](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me)来正确调用的方法。

[!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../code-quality/codesnippet/VisualBasic/ca1816-call-gc-suppressfinalize-correctly_2.vb)]
[!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../code-quality/codesnippet/CSharp/ca1816-call-gc-suppressfinalize-correctly_2.cs)]

## <a name="related-rules"></a>相关规则

- [CA2215Dispose 方法应调用基类 dispose](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)
- [CA2216可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>请参阅

- [Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)