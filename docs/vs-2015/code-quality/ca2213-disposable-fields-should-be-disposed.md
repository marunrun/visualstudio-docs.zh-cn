---
title: CA2213:应释放可释放的字段 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cbb606729fe89eb5c2ebe3c814096ef39120836a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685260"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213:应释放可释放的字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 实现的类型<xref:System.IDisposable?displayProperty=fullName>声明还实现的类型的字段<xref:System.IDisposable>。 <xref:System.IDisposable.Dispose%2A>字段的方法不由调用<xref:System.IDisposable.Dispose%2A>声明类型的方法。

## <a name="rule-description"></a>规则说明
 一种类型负责释放所有非托管资源;这通过实现来实现<xref:System.IDisposable>。 此规则检查以查看是否可释放类型`T`声明字段`F`，它是可释放类型的实例`FT`。 每个字段`F`，规则将尝试查找调用`FT.Dispose`。 该规则会搜索调用的方法`T.Dispose`，和一个级别较低 (调用的方法调用的方法`FT.Dispose`)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请调用<xref:System.IDisposable.Dispose%2A>所实现的类型的字段上<xref:System.IDisposable>如果你负责分配和释放非托管的资源持有的字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 则可以安全地禁止显示此规则的警告，如果你负责不释放资源持有的字段，或如果调用<xref:System.IDisposable.Dispose%2A>在更深层次的调用规则检查级别上发生。

## <a name="example"></a>示例
 下面的示例演示一种类型`TypeA`，它实现<xref:System.IDisposable>(`FT`前面讨论)。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>示例
 下面的示例演示一种类型`TypeB`违反该规则通过声明一个字段`aFieldOfADisposableType`(`F`前面讨论中) 作为可释放类型 (`TypeA`) 而不调用<xref:System.IDisposable.Dispose%2A>字段上。 `TypeB` 对应于`T`前面讨论中。

 [!code-csharp[FxCop.Usage.IDisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableFields/cs/FxCop.Usage.IDisposableFields.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.IDisposable?displayProperty=fullName> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
