---
title: CA2115:使用本机资源时调用 GC.KeepAlive
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CallGCKeepAliveWhenUsingNativeResources
- CA2115
helpviewer_keywords:
- CA2115
- CallGCKeepAliveWhenUsingNativeResources
ms.assetid: f00a59a7-2c6a-4bbe-a1b3-7bf77d366f34
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 9a74f6313f90a31d43cf39443b1c44d78f0628f8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545184"
---
# <a name="ca2115-call-gckeepalive-when-using-native-resources"></a>CA2115:使用本机资源时调用 GC.KeepAlive

|||
|-|-|
|TypeName|CallGCKeepAliveWhenUsingNativeResources|
|CheckId|CA2115|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

在具有终结器的类型中声明的方法引用<xref:System.IntPtr?displayProperty=fullName>或<xref:System.UIntPtr?displayProperty=fullName>字段中，但不会调用<xref:System.GC.KeepAlive%2A?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明

如果在托管代码中对它没有更多的引用，垃圾回收将终止对象。 对对象的非托管的引用不会阻止垃圾回收。 该规则检测由于在非托管代码仍在使用非托管资源时终止该非托管资源而可能发生的错误。

此规则假定<xref:System.IntPtr>和<xref:System.UIntPtr>字段存储指向非托管资源。 因为终结器的用途是释放非托管的资源，该规则将假定终结器将释放指针字段指向非托管的资源。 此规则还假定该方法引用要传递到非托管代码的非托管的资源的指针字段。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此规则的冲突，添加对的调用<xref:System.GC.KeepAlive%2A>方法，传递的当前实例 (`this`中C#和C++) 作为参数。 将该调用放在最后一行代码后该对象必须防止垃圾回收。 在调用后立即<xref:System.GC.KeepAlive%2A>，该对象再次被视为准备好进行垃圾收集假定没有托管的引用关系。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

此规则可导致误报可能会导致一些假设。 可以安全地禁止显示此规则的警告，如果：

- 终结器不会释放的内容<xref:System.IntPtr>或<xref:System.UIntPtr>字段引用的方法。

- 该方法不会传递<xref:System.IntPtr>或<xref:System.UIntPtr>字段到非托管代码。

不包括它们之前仔细查看其他消息。 此规则检测到难以重现和调试的错误。

## <a name="example"></a>示例

在下面的示例中，`BadMethod` 不包含对 `GC.KeepAlive` 的调用，因此违反了此规则。 `GoodMethod` 包含更正后的代码。

> [!NOTE]
> 此示例是伪代码。 尽管代码编译和运行，但不引发警告是因为未创建或释放非托管的资源。

[!code-csharp[FxCop.Security.IntptrAndFinalize#1](../code-quality/codesnippet/CSharp/ca2115-call-gc-keepalive-when-using-native-resources_1.cs)]

## <a name="see-also"></a>请参阅

- <xref:System.GC.KeepAlive%2A?displayProperty=fullName>
- <xref:System.IntPtr?displayProperty=fullName>
- <xref:System.Object.Finalize%2A?displayProperty=fullName>
- <xref:System.UIntPtr?displayProperty=fullName>
- [Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)