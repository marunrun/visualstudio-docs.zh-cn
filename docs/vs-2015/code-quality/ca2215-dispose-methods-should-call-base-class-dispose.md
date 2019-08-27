---
title: CA2215:方法应调用基类 dispose |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bc934afd9289a6bce425084f3588a7e912baf9b9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681194"
---
# <a name="ca2215-dispose-methods-should-call-base-class-dispose"></a>CA2215:Dispose 方法应调用基类释放
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DisposeMethodsShouldCallBaseClassDispose|
|CheckId|CA2215|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 实现的类型<xref:System.IDisposable?displayProperty=fullName>还实现的类型继承<xref:System.IDisposable>。 <xref:System.IDisposable.Dispose%2A>继承的类型的方法不会调用<xref:System.IDisposable.Dispose%2A>父类型的方法。

## <a name="rule-description"></a>规则说明
 如果类型继承自可释放类型，它必须调用<xref:System.IDisposable.Dispose%2A>方法内其自身的基类型从<xref:System.IDisposable.Dispose%2A>方法。 调用基类方法 Dispose 可确保发布创建的基类型的任何资源。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请调用`base`。<xref:System.IDisposable.Dispose%2A> 在你<xref:System.IDisposable.Dispose%2A>方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 则可以安全地禁止显示此规则的警告，如果在调用`base`。<xref:System.IDisposable.Dispose%2A> 在更深层次的调用规则检查级别上发生。

## <a name="example"></a>示例
 下面的示例演示一种类型`TypeA`实现<xref:System.IDisposable>。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>示例
 下面的示例演示一种类型`TypeB`的继承自类型`TypeA`，并正确地调用其<xref:System.IDisposable.Dispose%2A>方法。

 [!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableBaseCalled/vb/FxCop.Usage.IDisposableBaseCalled.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.IDisposable?displayProperty=fullName> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
