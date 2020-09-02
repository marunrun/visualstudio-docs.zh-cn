---
title: CA1404：紧跟在 P 调用之后调用 GetLastError |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
helpviewer_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
ms.assetid: 52ae9eff-50f9-4b2f-8039-ca7e49fba88e
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 54ac9a4d56136d9e981ae038a0b219aa4cb4774e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544490"
---
# <a name="ca1404-call-getlasterror-immediately-after-pinvoke"></a>CA1404：紧接在 P/Invoke 之后调用 GetLastError
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|CallGetLastErrorImmediatelyAfterPInvoke|
|CheckId|CA1404|
|类别|Microsoft. 互操作性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 对 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A?displayProperty=fullName> 方法或等效的 Win32 函数进行调用 `GetLastError` ，并且紧靠在之前的调用不是平台调用方法。

## <a name="rule-description"></a>规则描述
 平台调用方法访问非托管代码，并使用 `Declare` 中的关键字 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 或特性来定义 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 。 通常，在失败时，非托管函数会调用 Win32 `SetLastError` 函数来设置与失败关联的错误代码。 Failed 函数的调用方调用 Win32 `GetLastError` 函数来检索错误代码，并确定失败的原因。 错误代码在每个线程的基础上维护，并在下一次调用时被覆盖 `SetLastError` 。 调用失败的平台调用方法后，托管代码可以通过调用方法来检索错误代码 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 。 由于错误代码可以由其他托管类库方法的内部调用覆盖，因此 `GetLastError` <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 应在平台调用方法调用之后立即调用或方法。

 规则将忽略对平台调用方法的调用和对的调用之间发生的对以下托管成员的调用 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 。 这些成员不会更改错误代码，并有助于确定一些平台调用方法调用是否成功。

- <xref:System.IntPtr.Zero?displayProperty=fullName>

- <xref:System.IntPtr.op_Equality%2A?displayProperty=fullName>

- <xref:System.IntPtr.op_Inequality%2A?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SafeHandle.IsInvalid%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将调用移到， <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 以便它紧跟在对平台调用方法的调用之后。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果平台调用方法调用和方法调用之间的代码 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 不能显式或隐式导致错误代码更改，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的方法和满足规则的方法。

 [!code-csharp[FxCop.Interoperability.LastErrorPInvoke#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LastErrorPInvoke/cs/FxCop.Interoperability.LastErrorPInvoke.cs#1)]
 [!code-vb[FxCop.Interoperability.LastErrorPInvoke#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LastErrorPInvoke/vb/FxCop.Interoperability.LastErrorPInvoke.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1060：将 P/Invoke 移动到 NativeMethods 类](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

 [CA1400： P/Invoke 入口点应该存在](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

 [CA1401： P/Invoke 应不可见](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

 [CA2101：为 P/Invoke 字符串参数指定封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

 [CA2205:使用 Win32 API 的托管等效项](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)
