---
title: CA1060:将 P-invoke 移动到 NativeMethods 类 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
helpviewer_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
ms.assetid: 06686c8c-6ad3-42f7-a355-cbaefa347cfc
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f47fa4326da9914171e5014decbd6d6923c2f02e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200482"
---
# <a name="ca1060-move-pinvokes-to-nativemethods-class"></a>CA1060:将 P/Invoke 移动到 NativeMethods 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MovePInvokesToNativeMethodsClass|
|CheckId|CA1060|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 方法使用平台调用服务访问非托管的代码并不是其中一个的成员**NativeMethods**类。

## <a name="rule-description"></a>规则说明
 平台调用方法，如那些使用标记<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>属性或通过使用定义的方法`Declare`中的关键字[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，访问非托管的代码。 这些方法应采用以下类之一：

- **NativeMethods** -此类不会取消对非托管的代码权限的堆栈审核。 (<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName>必须不应用于此类。)此类是可以任意位置使用，因为不会执行堆栈审核的方法。

- **SafeNativeMethods** -此类取消显示非托管的代码权限的堆栈审核。 (<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName>应用于此类。)此类是安全的任何人都可以调用的方法。 这些方法的调用方不需要执行全面的安全检查，以确保使用的安全性，因为方法都是无害的任何调用方。

- **UnsafeNativeMethods** -此类取消显示非托管的代码权限的堆栈审核。 (<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName>应用于此类。)此类适用于的方法具有潜在危险的。 这些方法中的任何调用方必须执行全面的安全检查，以确保使用的安全性，因为将执行没有堆栈遍历。

  这些类声明为`internal`(`Friend`，在 Visual Basic 中)，并声明私有构造函数，以防止从正在创建的新实例。 这些类中的方法应`static`并`internal`(`Shared`和`Friend`在 Visual Basic 中)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请将方法移动到相应**NativeMethods**类。 对于大多数应用程序，将 P/Invoke 移动到名为的新类**NativeMethods**就足够了。

 但是，如果你正在开发供其他应用程序中使用的库，则应考虑定义调用的其他两个类**SafeNativeMethods**并**UnsafeNativeMethods**。 这些类类似于**NativeMethods**类; 但是，它们都使用名为的特殊属性标记**SuppressUnmanagedCodeSecurityAttribute**。 应用此属性时，运行时不会执行完整的堆栈审核，以确保所有调用方拥有**UnmanagedCode**权限。 运行时通常执行此权限在启动时检查。 由于不执行检查，因此可以显著提高对这些非托管方法调用的性能，它还使具有有限的权限来调用这些方法的代码。

 但是，您应谨慎使用此属性。 如果实施错误可能会造成严重的安全隐患...

 有关如何实现方法的信息，请参阅**NativeMethods**示例中， **SafeNativeMethods**示例中，并且**UnsafeNativeMethods**示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例声明与此规则冲突的方法。 若要更正冲突**RemoveDirectory**应将 P/Invoke 移动到相应的类，用于存放仅 P/Invoke。

 [!code-csharp[FxCop.Design.DllImportNativeMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DllImportNativeMethods/cs/FxCop.Design.DllImportNativeMethods.cs#1)]
 [!code-vb[FxCop.Design.DllImportNativeMethods#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DllImportNativeMethods/vb/FxCop.Design.DllImportNativeMethods.vb#1)]

## <a name="nativemethods-example"></a>NativeMethods 示例

### <a name="description"></a>描述
 因为**NativeMethods**类不应使用标记**SuppressUnmanagedCodeSecurityAttribute**，将需要在其中放置的 P/Invoke **UnmanagedCode**权限。 由于大多数应用程序从本地计算机上运行，并且完全信任一起运行，这通常是没有问题。 但是，如果你正在开发可重用的库，则应考虑定义**SafeNativeMethods**或**UnsafeNativeMethods**类。

 下面的示例演示**Interaction.Beep**方法，用于包装**MessageBeep** user32.dll 函数。 **MessageBeep** P/Invoke 置于**NativeMethods**类。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.NativeMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethods/cs/FxCop.Design.NativeMethods.cs#1)]
 [!code-vb[FxCop.Design.NativeMethods#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethods/vb/FxCop.Design.NativeMethods.vb#1)]

## <a name="safenativemethods-example"></a>SafeNativeMethods 示例

### <a name="description"></a>描述
 P/Invoke 方法，可以向任何应用程序安全地公开和没有任何副作用应置于名为的类**SafeNativeMethods**。 不需要注意多也称为从并不一定按需的权限。

 下面的示例演示**Environment.TickCount**包装的属性**GetTickCount** kernel32.dll 的函数。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.NativeMethodsSafe#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsSafe/cs/FxCop.Design.NativeMethodsSafe.cs#1)]
 [!code-vb[FxCop.Design.NativeMethodsSafe#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsSafe/vb/FxCop.Design.NativeMethodsSafe.vb#1)]

## <a name="unsafenativemethods-example"></a>UnsafeNativeMethods 示例

### <a name="description"></a>描述
 P/Invoke 方法，不能安全地调用和任何可导致副作用应置于名为的类**UnsafeNativeMethods**。 应严格检查这些方法，以确保它们不公开给用户无意中。 该规则[CA2118:检查 SuppressUnmanagedCodeSecurityAttribute 用法](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)对此有所帮助。 或者，方法应具有另一个而不是所需的权限**UnmanagedCode**何时使用它们。

 下面的示例演示**Cursor.Hide**方法，用于包装**ShowCursor** user32.dll 函数。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.NativeMethodsUnsafe#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsUnsafe/cs/FxCop.Design.NativeMethodsUnsafe.cs#1)]
 [!code-vb[FxCop.Design.NativeMethodsUnsafe#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsUnsafe/vb/FxCop.Design.NativeMethodsUnsafe.vb#1)]

## <a name="see-also"></a>请参阅
 [设计警告](../code-quality/design-warnings.md)
