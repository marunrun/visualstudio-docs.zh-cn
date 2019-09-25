---
title: CA2215:Dispose 方法应调用基类释放
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2215
- DisposeMethodsShouldCallBaseClassDispose
- Dispose methods should call base class dispose
helpviewer_keywords:
- DisposeMethodsShouldCallBaseClassDispose
- CA2215
ms.assetid: c772e7a6-a87e-425c-a70e-912664ae9042
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 468b63ca554ea126bbd621a2502e54540e6ed068
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231285"
---
# <a name="ca2215-dispose-methods-should-call-base-class-dispose"></a>CA2215:Dispose 方法应调用基类释放

|||
|-|-|
|TypeName|DisposeMethodsShouldCallBaseClassDispose|
|CheckId|CA2215|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因
实现<xref:System.IDisposable?displayProperty=fullName>的类型继承自也实现<xref:System.IDisposable>的类型。 继承类型的<xref:System.IDisposable.Dispose%2A>方法不调用父类型的方法。 <xref:System.IDisposable.Dispose%2A>

## <a name="rule-description"></a>规则说明
如果某个类型继承自可释放类型，则它必须从<xref:System.IDisposable.Dispose%2A>其自身<xref:System.IDisposable.Dispose%2A>的方法中调用基类型的方法。 调用基类型方法 Dispose 可确保释放基类型创建的所有资源。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突， `base`请调用。<xref:System.IDisposable.Dispose%2A> 在您<xref:System.IDisposable.Dispose%2A>的方法中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果调用`base`，则可以安全地禁止显示此规则发出的警告。<xref:System.IDisposable.Dispose%2A> 在比规则检查更深入的调用级别上发生。

## <a name="example"></a>示例
下面的示例演示实现`TypeA` <xref:System.IDisposable>的类型。

[!code-csharp[FxCop.Usage.IDisposablePattern#1](../code-quality/codesnippet/CSharp/ca2215-dispose-methods-should-call-base-class-dispose_1.cs)]

## <a name="example"></a>示例
下面的示例演示从类型`TypeB` `TypeA`继承并正确调用其<xref:System.IDisposable.Dispose%2A>方法的类型。

[!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../code-quality/codesnippet/VisualBasic/ca2215-dispose-methods-should-call-base-class-dispose_2.vb)]

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable?displayProperty=fullName>
- [释放模式](/dotnet/standard/design-guidelines/dispose-pattern)