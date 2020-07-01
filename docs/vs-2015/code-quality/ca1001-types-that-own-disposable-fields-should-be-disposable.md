---
title: CA1001：拥有可释放字段的类型应该是可释放的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dab4532f082bd81eaa7b812eb038c5957636d453
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548312"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001:具有可释放字段的类型应该是可释放的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|TypesThatOwnDisposableFieldsShouldBeDisposable|
|CheckId|CA1001|
|Category|Microsoft. Design|
|是否重大更改|不间断-如果类型在程序集外部不可见。<br /><br /> 如果该类型在程序集外可见，则为。|

## <a name="cause"></a>原因
 类声明并实现属于 <xref:System.IDisposable?displayProperty=fullName> 类型并且类不实现的实例字段 <xref:System.IDisposable> 。

## <a name="rule-description"></a>规则描述
 类实现 <xref:System.IDisposable> 接口，以释放其拥有的非托管资源。 类型为的实例字段 <xref:System.IDisposable> 指示该字段拥有非托管资源。 声明字段的类 <xref:System.IDisposable> 间接拥有非托管资源，并且应实现 <xref:System.IDisposable> 接口。 如果类不直接拥有任何非托管资源，则它不应实现终结器。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请在方法中实现 <xref:System.IDisposable> 和，并 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 调用 <xref:System.IDisposable.Dispose%2A> 字段的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个与规则冲突的类和一个通过实现来满足规则的类 <xref:System.IDisposable> 。 类不实现终结器，因为该类不直接拥有任何非托管资源。

 [!code-csharp[FxCop.Design.DisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/cs/FxCop.Design.DisposableFields.cs#1)]
 [!code-vb[FxCop.Design.DisposableFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/vb/FxCop.Design.DisposableFields.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2213:应释放可释放的字段](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

 [CA2216:可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA2215:Dispose 方法应调用基类释放](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA1049:拥有本机资源的类型应是可释放的](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)
