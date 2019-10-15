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
ms.openlocfilehash: 03b8d222fc2349022ef324c9905279677fc86849
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72306117"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049:拥有本机资源的类型应是可释放的

|||
|-|-|
|TypeName|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因

类型引用 @no__t 0 字段、@no__t 1 字段或 @no__t 2 字段，但不实现 <xref:System.IDisposable?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明

此规则假定 <xref:System.IntPtr>、<xref:System.UIntPtr> 和 <xref:System.Runtime.InteropServices.HandleRef> 字段存储指向非托管资源的指针。 分配非托管资源的类型应实现 <xref:System.IDisposable>，使调用方能够按需释放这些资源，并缩短包含资源的对象的生存期。

用于清理非托管资源的建议设计模式是通过分别使用 @no__t 0 方法和 @no__t 方法，同时提供隐式和显式方式来释放这些资源。 在确定无法再访问对象之后，垃圾回收器在某个不确定的时间调用对象的 @no__t 0 方法。 调用 <xref:System.Object.Finalize%2A> 后，需要额外的垃圾回收来释放对象。 @No__t-0 方法使调用方能够按需显式释放资源，而不是在离开垃圾回收器时释放资源。 清除非托管资源后，<xref:System.IDisposable.Dispose%2A> 应调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 方法，使垃圾回收器知道不再需要调用 <xref:System.Object.Finalize%2A>;这样就无需进行额外的垃圾回收，缩短了对象的生存期。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请实现 <xref:System.IDisposable>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果类型不引用非托管资源，则可以安全地禁止显示此规则发出的警告。 否则，请不要禁止显示此规则发出的警告，因为未能实现 <xref:System.IDisposable> 会导致非托管资源变为不可用或未充分利用。

## <a name="example"></a>示例
下面的示例演示实现 <xref:System.IDisposable> 以清理非托管资源的类型。

[!code-csharp[FxCop.Design.UnmanagedResources#1](../code-quality/codesnippet/CSharp/ca1049-types-that-own-native-resources-should-be-disposable_1.cs)]
[!code-vb[FxCop.Design.UnmanagedResources#1](../code-quality/codesnippet/VisualBasic/ca1049-types-that-own-native-resources-should-be-disposable_1.vb)]

## <a name="related-rules"></a>相关规则
[CA2115：调用 GC。使用本机资源时 KeepAlive no__t-0

[CA1816：调用 GC。Gc.suppressfinalize 正确 @ no__t-0

[CA2216：可释放类型应声明终结器 @ no__t-0

[CA1001：具有可释放字段的类型应该是可释放的](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>请参阅

- [清理未托管资源](/dotnet/standard/garbage-collection/unmanaged)（清理未托管资源）
- [Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)