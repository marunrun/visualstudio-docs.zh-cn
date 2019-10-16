---
title: CA1001：具有可释放字段的类型应该是可释放的
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
ms.openlocfilehash: e8f2f313dad5f412a1a4d983d785caad5e6022a8
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349451"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001：具有可释放字段的类型应该是可释放的

|||
|-|-|
|TypeName|TypesThatOwnDisposableFieldsShouldBeDisposable|
|CheckId|CA1001|
|类别|Microsoft. Design|
|重大更改|不间断-如果类型在程序集外部不可见。<br /><br /> 如果该类型在程序集外可见，则为。|

## <a name="cause"></a>原因
类声明并实现一个实例字段，该字段是 @no__t 类型的类型，并且该类不实现 @no__t。

## <a name="rule-description"></a>规则说明
类实现 <xref:System.IDisposable> 接口，以释放其拥有的非托管资源。 作为 @no__t 类型的实例字段指示该字段拥有非托管资源。 声明 @no__t 0 字段的类间接拥有非托管资源，并且应实现 <xref:System.IDisposable> 接口。 如果类不直接拥有任何非托管资源，则它不应实现终结器。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请实现 <xref:System.IDisposable>，并从 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 方法调用字段的 <xref:System.IDisposable.Dispose%2A> 方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示一个与规则冲突的类，以及一个通过实现 <xref:System.IDisposable> 满足规则的类。 类不实现终结器，因为该类不直接拥有任何非托管资源。

[!code-vb[FxCop.Design.DisposableFields#1](../code-quality/codesnippet/VisualBasic/ca1001-types-that-own-disposable-fields-should-be-disposable_1.vb)]
[!code-csharp[FxCop.Design.DisposableFields#1](../code-quality/codesnippet/CSharp/ca1001-types-that-own-disposable-fields-should-be-disposable_1.cs)]

## <a name="related-rules"></a>相关规则
[CA2213：应释放可释放的字段](../code-quality/ca2213.md)

[CA2216：可释放类型应声明终结器](../code-quality/ca2216.md)

[CA2215：Dispose 方法应调用基类 Dispose](../code-quality/ca2215.md)

[CA1049：拥有本机资源的类型应可释放](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)