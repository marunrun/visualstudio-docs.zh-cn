---
title: CA2205:使用 Win32 API 的托管等效项
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
helpviewer_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
ms.assetid: 1c65ab59-3e50-4488-a727-3969c7f6cbe4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 99d53296ad72aef1910a39299be64c7cb03dd49a
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714714"
---
# <a name="ca2205-use-managed-equivalents-of-win32-api"></a>CA2205:使用 Win32 API 的托管等效项

|||
|-|-|
|TypeName|UseManagedEquivalentsOfWin32Api|
|CheckId|CA2205|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

平台调用定义方法和.NET 中存在具有等效功能的方法。

## <a name="rule-description"></a>规则说明

平台调用方法用于调用非托管的 DLL 函数，并使用定义<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>属性，或`Declare`在 Visual Basic 中的关键字。 定义不正确的平台调用方法可能会导致运行时异常到由于问题，例如名不符实了函数、 错误的参数和返回值数据类型和不正确的字段规范，如调用约定和字符映射设置。 如果可用，很容易调用等效的托管的方法比定义并直接调用非托管的方法更简单、 更少出错。 调用平台调用方法可能还会导致需要解决的其他安全问题。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此规则的冲突，请对非托管函数的调用替换为通过调用其托管等同项。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果建议的替代方法不提供所需的功能，禁止显示此规则的警告。

## <a name="example"></a>示例

下面的示例演示一个平台的调用违反了此规则的方法定义。 此外，对平台调用调用方法并显示等效的托管的方法。

[!code-csharp[FxCop.Usage.ManagedEquivalents#1](../code-quality/codesnippet/CSharp/ca2205-use-managed-equivalents-of-win32-api_1.cs)]
[!code-vb[FxCop.Usage.ManagedEquivalents#1](../code-quality/codesnippet/VisualBasic/ca2205-use-managed-equivalents-of-win32-api_1.vb)]

## <a name="related-rules"></a>相关的规则

- [CA1404:紧接在 P/Invoke 之后调用 GetLastError](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)
- [CA1060:将 P/Invoke 移动到 NativeMethods 类](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)
- [CA1400:P/Invoke 入口点应该存在](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)
- [CA1401:P/Invokes 应该是不可见](../code-quality/ca1401-p-invokes-should-not-be-visible.md)
- [CA2101:指定对 P/Invoke 字符串自变量封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)