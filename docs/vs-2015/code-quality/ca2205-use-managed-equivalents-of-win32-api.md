---
title: CA2205：使用 Win32 API 的托管等效项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
helpviewer_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
ms.assetid: 1c65ab59-3e50-4488-a727-3969c7f6cbe4
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 85e27ab04ca81f5513a0b09bc41548f4a7c2430d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547675"
---
# <a name="ca2205-use-managed-equivalents-of-win32-api"></a>CA2205:使用 Win32 API 的托管等效项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|UseManagedEquivalentsOfWin32Api|
|CheckId|CA2205|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 定义了平台调用方法，并且类库中存在具有等效功能的方法 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

## <a name="rule-description"></a>规则描述
 平台调用方法用于调用非托管 DLL 函数并使用 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 特性或 `Declare` Visual Basic 中的关键字进行定义。 错误定义的平台调用方法可能会导致运行时异常，原因是 misnamed 函数、参数和返回值数据类型的错误映射以及错误的字段规范（如调用约定和字符集）。 如果可用，调用等效的托管方法比直接定义和调用非托管方法更简单且更少出错。 调用平台调用方法还可能导致其他需要解决的安全问题。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将对非托管函数的调用替换为对其托管等效项的调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果建议的替换方法未提供所需的功能，则禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了违反规则的平台调用方法定义。 此外，还会显示对平台调用方法和等效托管方法的调用。

 [!code-csharp[FxCop.Usage.ManagedEquivalents#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ManagedEquivalents/cs/FxCop.Usage.ManagedEquivalents.cs#1)]
 [!code-vb[FxCop.Usage.ManagedEquivalents#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ManagedEquivalents/vb/FxCop.Usage.ManagedEquivalents.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1404：紧接在 P/Invoke 之后调用 GetLastError](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)

 [CA1060：将 P/Invoke 移动到 NativeMethods 类](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

 [CA1400： P/Invoke 入口点应该存在](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

 [CA1401： P/Invoke 应不可见](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

 [CA2101：为 P/Invoke 字符串参数指定封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)
