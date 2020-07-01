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
ms.openlocfilehash: 4197c2faaf4aa23db930a9019538592326a84116
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534376"
---
# <a name="ca2215-dispose-methods-should-call-base-class-dispose"></a>CA2215:Dispose 方法应调用基类释放
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DisposeMethodsShouldCallBaseClassDispose|
|CheckId|CA2215|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 实现的类型 <xref:System.IDisposable?displayProperty=fullName> 继承自也实现的类型 <xref:System.IDisposable> 。 <xref:System.IDisposable.Dispose%2A>继承类型的方法不调用 <xref:System.IDisposable.Dispose%2A> 父类型的方法。

## <a name="rule-description"></a>规则描述
 如果某个类型继承自可释放类型，则它必须 <xref:System.IDisposable.Dispose%2A> 从其自身的方法中调用基类型的方法 <xref:System.IDisposable.Dispose%2A> 。 调用基类型方法 Dispose 可确保释放基类型创建的所有资源。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请调用 `base` 。<xref:System.IDisposable.Dispose%2A> 在您的 <xref:System.IDisposable.Dispose%2A> 方法中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果调用，则可以安全地禁止显示此规则发出的警告 `base` 。<xref:System.IDisposable.Dispose%2A> 在比规则检查更深入的调用级别上发生。

## <a name="example"></a>示例
 下面的示例演示实现的类型 `TypeA` <xref:System.IDisposable> 。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>示例
 下面的示例演示 `TypeB` 从类型继承 `TypeA` 并正确调用其方法的类型 <xref:System.IDisposable.Dispose%2A> 。

 [!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableBaseCalled/vb/FxCop.Usage.IDisposableBaseCalled.vb#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.IDisposable?displayProperty=fullName> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
