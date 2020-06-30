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
ms.openlocfilehash: 887600bad0c3d05ff78050aa4449cf49dc882027
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534571"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213:应释放可释放的字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|Category|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 一种类型，该类型实现 <xref:System.IDisposable?displayProperty=fullName> 也实现的类型的字段 <xref:System.IDisposable> 。 该 <xref:System.IDisposable.Dispose%2A> 字段的方法不由 <xref:System.IDisposable.Dispose%2A> 声明类型的方法调用。

## <a name="rule-description"></a>规则描述
 类型负责释放其所有非托管资源;这是通过实现实现的 <xref:System.IDisposable> 。 此规则检查可释放类型是否 `T` 声明一个字段 `F` ，该字段是可释放类型的实例 `FT` 。 对于每个字段 `F` ，该规则将尝试查找对的调用 `FT.Dispose` 。 此规则将搜索由调用的方法 `T.Dispose` ，一个级别较低（由调用的方法调用的方法 `FT.Dispose` ）。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请对 <xref:System.IDisposable.Dispose%2A> 属于实现的类型的字段调用（ <xref:System.IDisposable> 如果你负责分配和释放字段所持有的非托管资源）。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果你不负责释放字段持有的资源，或者如果调用 <xref:System.IDisposable.Dispose%2A> 发生在比规则检查更深入的调用级别上，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个 `TypeA` 实现的类型 <xref:System.IDisposable> （ `FT` 在上一讨论中）。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>示例
 下面的示例演示一个类型 `TypeB` ，该类型违反此规则，方法是将字段 `aFieldOfADisposableType` （ `F` 在上一讨论中）声明为可释放类型（ `TypeA` ），而不是 <xref:System.IDisposable.Dispose%2A> 对字段调用。 `TypeB`与 `T` 上一讨论中的相对应。

 [!code-csharp[FxCop.Usage.IDisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableFields/cs/FxCop.Usage.IDisposableFields.cs#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.IDisposable?displayProperty=fullName> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
