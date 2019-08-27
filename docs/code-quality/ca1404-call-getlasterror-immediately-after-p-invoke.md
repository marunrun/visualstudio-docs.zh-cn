---
title: CA1404:紧接在 P-Invoke 之后调用 GetLastError
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
ms.openlocfilehash: 03add1625c4d59bb180f9f0f08692e67bee8047b
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922068"
---
# <a name="ca1404-call-getlasterror-immediately-after-pinvoke"></a>CA1404:紧接在 P/Invoke 之后调用 GetLastError

|||
|-|-|
|TypeName|CallGetLastErrorImmediatelyAfterPInvoke|
|CheckId|CA1404|
|类别|Microsoft.Interoperability|
|是否重大更改|不间断|

## <a name="cause"></a>原因

对<xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A?displayProperty=fullName>方法或等效的 Win32 `GetLastError`函数进行调用, 并且紧靠在之前的调用不是平台调用方法。

## <a name="rule-description"></a>规则说明
平台调用方法访问非托管代码, 并使用中`Declare` [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]的关键字或<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>特性来定义。 通常, 在失败时, 非托管函数会`SetLastError`调用 Win32 函数来设置与失败关联的错误代码。 Failed 函数的调用方调用 Win32 `GetLastError`函数来检索错误代码, 并确定失败的原因。 错误代码在每个线程的基础上维护, 并在下一次调用`SetLastError`时被覆盖。 调用失败的平台调用方法后, 托管代码可以通过调用<xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>方法来检索错误代码。 由于错误代码可以由其他托管类库方法的内部调用覆盖, `GetLastError`因此应在平台调用方法调用之后立即调用或<xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>方法。

规则将忽略对平台调用方法的调用和对<xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>的调用之间发生的对以下托管成员的调用。 这些成员不会更改错误代码, 并有助于确定一些平台调用方法调用是否成功。

- <xref:System.IntPtr.Zero?displayProperty=fullName>

- <xref:System.IntPtr.op_Equality%2A?displayProperty=fullName>

- <xref:System.IntPtr.op_Inequality%2A?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SafeHandle.IsInvalid%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将调用<xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>移到, 以便它紧跟在对平台调用方法的调用之后。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果平台调用方法调用和<xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>方法调用之间的代码不能显式或隐式导致错误代码更改, 则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则的方法和满足规则的方法。

[!code-vb[FxCop.Interoperability.LastErrorPInvoke#1](../code-quality/codesnippet/VisualBasic/ca1404-call-getlasterror-immediately-after-p-invoke_1.vb)]
[!code-csharp[FxCop.Interoperability.LastErrorPInvoke#1](../code-quality/codesnippet/CSharp/ca1404-call-getlasterror-immediately-after-p-invoke_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1060将 P/Invoke 移动到 NativeMethods 类](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

[CA1400P/Invoke 入口点应该存在](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

[CA1401P/Invoke 不应是可见的](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

[CA2101指定对 P/Invoke 字符串参数进行封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

[CA2205使用 Win32 API 的托管等效项](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)