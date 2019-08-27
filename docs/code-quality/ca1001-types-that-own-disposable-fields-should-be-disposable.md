---
title: CA1001:具有可释放字段的类型应该是可释放的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: fae67f8c1ffa3b4e6d7cc2f0fbbaf670733f9ff4
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923313"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001:具有可释放字段的类型应该是可释放的

|||
|-|-|
|TypeName|TypesThatOwnDisposableFieldsShouldBeDisposable|
|CheckId|CA1001|
|类别|Microsoft.Design|
|是否重大更改|不间断-如果类型在程序集外部不可见。<br /><br /> 如果该类型在程序集外可见, 则为。|

## <a name="cause"></a>原因
类声明并实现属于<xref:System.IDisposable?displayProperty=fullName>类型并且类不实现<xref:System.IDisposable>的实例字段。

## <a name="rule-description"></a>规则说明
类实现<xref:System.IDisposable>接口, 以释放其拥有的非托管资源。 <xref:System.IDisposable>类型为的实例字段指示该字段拥有非托管资源。 声明<xref:System.IDisposable>字段的类间接拥有非托管资源, 并且应<xref:System.IDisposable>实现接口。 如果类不直接拥有任何非托管资源, 则它不应实现终结器。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, <xref:System.IDisposable>请在<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>方法中实现和<xref:System.IDisposable.Dispose%2A> , 并调用字段的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示一个与规则冲突的类和一个通过实现<xref:System.IDisposable>来满足规则的类。 类不实现终结器, 因为该类不直接拥有任何非托管资源。

[!code-vb[FxCop.Design.DisposableFields#1](../code-quality/codesnippet/VisualBasic/ca1001-types-that-own-disposable-fields-should-be-disposable_1.vb)]
[!code-csharp[FxCop.Design.DisposableFields#1](../code-quality/codesnippet/CSharp/ca1001-types-that-own-disposable-fields-should-be-disposable_1.cs)]

## <a name="related-rules"></a>相关规则
[CA2213：应释放可释放的字段](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

[CA2216可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

[CA2215Dispose 方法应调用基类 dispose](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

[CA1049拥有本机资源的类型应是可释放的](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)