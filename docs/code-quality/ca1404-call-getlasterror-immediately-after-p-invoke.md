---
title: CA1404：紧接在 P-Invoke 之后调用 GetLastError
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
helpviewer_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
ms.assetid: 52ae9eff-50f9-4b2f-8039-ca7e49fba88e
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 6529adafa7384bf8b51444dd2cc81b9952b6b57c
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349010"
---
# <a name="ca1404-call-getlasterror-immediately-after-pinvoke"></a>CA1404：紧接在 P/Invoke 之后调用 GetLastError

|||
|-|-|
|TypeName|CallGetLastErrorImmediatelyAfterPInvoke|
|CheckId|CA1404|
|类别|Microsoft. 互操作性|
|重大更改|不间断|

## <a name="cause"></a>原因

调用 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A?displayProperty=fullName> 方法或等效的 Win32 `GetLastError` 函数，并且紧靠在之前的调用不是平台调用方法。

## <a name="rule-description"></a>规则说明
平台调用方法访问非托管代码，并使用 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中的 @no__t 关键字或 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 特性来定义。 通常，在失败时，非托管函数会调用 Win32 `SetLastError` 函数来设置与失败关联的错误代码。 Failed 函数的调用方调用 Win32 `GetLastError` 函数来检索错误代码，并确定失败的原因。 错误代码在每个线程的基础上维护，并在下一次调用 @no__t 时被覆盖。 调用失败的平台调用方法后，托管代码可以通过调用 @no__t 的方法来检索错误代码。 由于错误代码可以被其他托管类库方法中的内部调用所覆盖，因此应在平台调用方法调用之后立即调用 `GetLastError` 或 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 方法。

当对平台调用方法的调用与对 @no__t 的调用之间发生时，规则将忽略对以下托管成员的调用。 这些成员不会更改错误代码，并有助于确定一些平台调用方法调用是否成功。

- <xref:System.IntPtr.Zero?displayProperty=fullName>

- <xref:System.IntPtr.op_Equality%2A?displayProperty=fullName>

- <xref:System.IntPtr.op_Inequality%2A?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SafeHandle.IsInvalid%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将对的调用移动到 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>，使其立即遵循对平台调用方法的调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果平台调用方法调用和 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 方法调用之间的代码不能显式或隐式导致错误代码更改，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则的方法和满足规则的方法。

[!code-vb[FxCop.Interoperability.LastErrorPInvoke#1](../code-quality/codesnippet/VisualBasic/ca1404-call-getlasterror-immediately-after-p-invoke_1.vb)]
[!code-csharp[FxCop.Interoperability.LastErrorPInvoke#1](../code-quality/codesnippet/CSharp/ca1404-call-getlasterror-immediately-after-p-invoke_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1060：将 P/Invoke 移动到](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md) NativeMethods 类

[CA1400：P/Invoke 入口点应该存在](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

[CA1401：P/Invokes 应为不可见](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

[CA2101：指定对 P/Invoke 字符串参数进行封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

[CA2205：使用 Win32 API 的托管等效项](../code-quality/ca2205.md)