---
title: CA1049:拥有本机资源的类型应是可释放的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1049
- TypesThatOwnNativeResourcesShouldBeDisposable
helpviewer_keywords:
- TypesThatOwnNativeResourcesShouldBeDisposable
- CA1049
ms.assetid: 084e587d-0e45-4092-b767-49eed30d6a35
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- cplusplus
ms.openlocfilehash: ef7b72eade7ea8e4486d5c317c06026bb4d0b95f
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235734"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049:拥有本机资源的类型应是可释放的

|||
|-|-|
|TypeName|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因

类型引用<xref:System.IntPtr?displayProperty=fullName>字段<xref:System.UIntPtr?displayProperty=fullName> 、字段或<xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>字段，但不实现<xref:System.IDisposable?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明

此规则假定、 <xref:System.IntPtr> <xref:System.UIntPtr>和<xref:System.Runtime.InteropServices.HandleRef>字段存储指向非托管资源的指针。 分配非托管资源的类型应<xref:System.IDisposable>实现，使调用方能够按需释放这些资源，并缩短包含资源的对象的生存期。

用于清理非托管资源的建议设计模式是通过分别使用<xref:System.Object.Finalize%2A?displayProperty=fullName>方法<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>和方法提供隐式和显式方式来释放这些资源。 在确定无法再访问<xref:System.Object.Finalize%2A>对象之后，垃圾回收器在某个不确定的时间调用对象的方法。 调用<xref:System.Object.Finalize%2A>后，需要额外的垃圾回收来释放对象。 此<xref:System.IDisposable.Dispose%2A>方法允许调用方按需显式释放资源，而不是在离开垃圾回收器时释放资源。 清除非托管资源后， <xref:System.IDisposable.Dispose%2A>应<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>调用方法让垃圾回收器知道<xref:System.Object.Finalize%2A>不再需要调用; 这无需进行额外的垃圾回收，缩短了对象的生存期。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突， <xref:System.IDisposable>请实现。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果类型不引用非托管资源，则可以安全地禁止显示此规则发出的警告。 否则，请不要禁止显示此规则发出的警告，因为未能<xref:System.IDisposable>实现可能会导致非托管资源变为不可用或未充分利用。

## <a name="example"></a>示例
下面的示例演示实现<xref:System.IDisposable>的用于清理非托管资源的类型。

[!code-csharp[FxCop.Design.UnmanagedResources#1](../code-quality/codesnippet/CSharp/ca1049-types-that-own-native-resources-should-be-disposable_1.cs)]
[!code-vb[FxCop.Design.UnmanagedResources#1](../code-quality/codesnippet/VisualBasic/ca1049-types-that-own-native-resources-should-be-disposable_1.vb)]

## <a name="related-rules"></a>相关规则
[CA2115调用 GC。使用本机资源时 KeepAlive](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

[CA1816调用 GC。Gc.suppressfinalize 正确](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

[CA2216可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

[CA1001：具有可释放字段的类型应该是可释放的](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>请参阅

- [清理未托管资源](/dotnet/standard/garbage-collection/unmanaged)（清理未托管资源）
- [释放模式](/dotnet/standard/design-guidelines/dispose-pattern)