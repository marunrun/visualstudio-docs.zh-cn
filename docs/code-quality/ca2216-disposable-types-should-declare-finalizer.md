---
title: CA2216:可释放类型应声明终结器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DisposableTypesShouldDeclareFinalizer
- CA2216
helpviewer_keywords:
- CA2216
- DisposableTypesShouldDeclareFinalizer
ms.assetid: 0cabcc5e-b526-452b-8c2a-0cbe3b93c0ef
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ac52bdb17aeb7d04e434d2b02ff9a905eab49a2
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305928"
---
# <a name="ca2216-disposable-types-should-declare-finalizer"></a>CA2216:可释放类型应声明终结器

|||
|-|-|
|TypeName|DisposableTypesShouldDeclareFinalizer|
|CheckId|CA2216|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

一个实现 <xref:System.IDisposable?displayProperty=fullName> 的类型，并且具有建议使用非托管资源的字段，不按 <xref:System.Object.Finalize%2A?displayProperty=fullName> 所述实现终结器。

## <a name="rule-description"></a>规则说明

如果可释放类型包含以下类型的字段，则会报告此规则的冲突：

- <xref:System.IntPtr?displayProperty=fullName>

- <xref:System.UIntPtr?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请实现调用 <xref:System.IDisposable.Dispose%2A> 方法的终结器。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果该类型未实现 <xref:System.IDisposable> 以释放非托管资源，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示违反此规则的类型。

[!code-csharp[FxCop.Usage.DisposeNoFinalize#1](../code-quality/codesnippet/CSharp/ca2216-disposable-types-should-declare-finalizer_1.cs)]

## <a name="related-rules"></a>相关规则

[CA2115：调用 GC。使用本机资源时 KeepAlive no__t-0

[CA1816：调用 GC。Gc.suppressfinalize 正确 @ no__t-0

[CA1049：拥有本机资源的类型应为可释放 @ no__t-0

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable?displayProperty=fullName>
- <xref:System.IntPtr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>
- <xref:System.UIntPtr?displayProperty=fullName>
- <xref:System.Object.Finalize%2A?displayProperty=fullName>
- [Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)