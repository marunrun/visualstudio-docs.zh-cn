---
title: CA2215： Dispose 方法应调用基类 Dispose |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2215
- DisposeMethodsShouldCallBaseClassDispose
- Dispose methods should call base class dispose
helpviewer_keywords:
- DisposeMethodsShouldCallBaseClassDispose
- CA2215
ms.assetid: c772e7a6-a87e-425c-a70e-912664ae9042
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 89f3705169fb9d28a1ec773671d460f00b98d892
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662855"
---
# <a name="ca2215-dispose-methods-should-call-base-class-dispose"></a>CA2215：Dispose 方法应调用基类的 Dispose
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DisposeMethodsShouldCallBaseClassDispose|
|CheckId|CA2215|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 实现 <xref:System.IDisposable?displayProperty=fullName> 的类型继承自还实现 <xref:System.IDisposable> 的类型。 继承类型的 <xref:System.IDisposable.Dispose%2A> 方法不会调用父类型的 <xref:System.IDisposable.Dispose%2A> 方法。

## <a name="rule-description"></a>规则说明
 如果某个类型继承自一个可释放类型，则该类型必须从其自身的 <xref:System.IDisposable.Dispose%2A> 方法中调用基类型的 <xref:System.IDisposable.Dispose%2A> 方法。 调用基类型方法 Dispose 可确保释放基类型创建的所有资源。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请调用 `base`。<xref:System.IDisposable.Dispose%2A> 在 <xref:System.IDisposable.Dispose%2A> 方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果调用 `base`，则可以安全地禁止显示此规则发出的警告。<xref:System.IDisposable.Dispose%2A> 在比规则检查更深入的调用级别上发生。

## <a name="example"></a>示例
 下面的示例演示实现 <xref:System.IDisposable> `TypeA` 类型。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>示例
 下面的示例演示从类型继承的类型 `TypeB` `TypeA` 并正确调用其 <xref:System.IDisposable.Dispose%2A> 方法。

 [!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableBaseCalled/vb/FxCop.Usage.IDisposableBaseCalled.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.IDisposable?displayProperty=fullName> [Dispose 模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
