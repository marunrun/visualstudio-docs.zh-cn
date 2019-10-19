---
title: CA1049：拥有本机资源的类型应是可释放的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1049
- TypesThatOwnNativeResourcesShouldBeDisposable
helpviewer_keywords:
- TypesThatOwnNativeResourcesShouldBeDisposable
- CA1049
ms.assetid: 084e587d-0e45-4092-b767-49eed30d6a35
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aaaf95346c51e2cb5cadb01a39e482bb508bc764
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668907"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049：拥有本机资源的类型应是可释放的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型引用 <xref:System.IntPtr?displayProperty=fullName> 字段、<xref:System.UIntPtr?displayProperty=fullName> 字段或 <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName> 字段，但不实现 <xref:System.IDisposable?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 此规则假定 <xref:System.IntPtr>、<xref:System.UIntPtr> 和 <xref:System.Runtime.InteropServices.HandleRef> 字段存储指向非托管资源的指针。 分配非托管资源的类型应实现 <xref:System.IDisposable>，使调用方能够按需释放这些资源，并缩短包含资源的对象的生存期。

 用于清理非托管资源的建议设计模式是通过分别使用 <xref:System.Object.Finalize%2A?displayProperty=fullName> 方法和 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 方法提供隐式和显式方式来释放这些资源。 在确定无法再访问对象之后，垃圾回收器在某个不确定的时间调用对象的 <xref:System.Object.Finalize%2A> 方法。 调用 <xref:System.Object.Finalize%2A> 后，需要额外的垃圾回收来释放对象。 @No__t_0 方法使调用方能够按需显式释放资源，而不是在离开垃圾回收器时释放资源。 清理非托管资源后，<xref:System.IDisposable.Dispose%2A> 应调用 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> 方法，使垃圾回收器知道不再需要调用 <xref:System.Object.Finalize%2A>;这样就无需进行额外的垃圾回收，缩短了对象的生存期。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请实现 <xref:System.IDisposable>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果类型不引用非托管资源，则可以安全地禁止显示此规则发出的警告。 否则，请不要禁止显示此规则发出的警告，因为未能实现 <xref:System.IDisposable> 会导致非托管资源变为不可用或未充分利用。

## <a name="example"></a>示例
 下面的示例演示实现 <xref:System.IDisposable> 以清理非托管资源的类型。

 [!code-csharp[FxCop.Design.UnmanagedResources#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/cs/FxCop.Design.UnmanagedResources.cs#1)]
 [!code-vb[FxCop.Design.UnmanagedResources#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/vb/FxCop.Design.UnmanagedResources.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2115：使用本机资源时调用 GC.KeepAlive](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

 [CA1816：正确调用 GC.SuppressFinalize](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

 [CA2216：可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA1001：具有可释放字段的类型应该是可释放的](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>请参阅
  [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
