---
title: CA1414:用 MarshalAs 标记布尔型 P-Invoke 参数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
helpviewer_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
ms.assetid: c0c84cf5-7701-4897-9114-66fc4b895699
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 22e62a1e3209399be4b10a3ec28db4afdd6f0f20
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234676"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414:用 MarshalAs 标记布尔型 P/Invoke 参数

|||
|-|-|
|TypeName|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|类别|Microsoft.Interoperability|
|重大更改|重大|

## <a name="cause"></a>原因
平台调用方法声明包括<xref:System.Boolean?displayProperty=fullName>参数或返回值， <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName>但特性不应用于参数或返回值。

## <a name="rule-description"></a>规则说明
平台调用方法访问非托管代码，并通过使用或`Declare` <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]的关键字定义。 <xref:System.Runtime.InteropServices.MarshalAsAttribute>指定用于在托管代码和非托管代码之间转换数据类型的封送处理行为。 许多简单的数据类型（例如<xref:System.Byte?displayProperty=fullName>和<xref:System.Int32?displayProperty=fullName>）在非托管代码中具有单个表示形式，并且不需要指定其封送处理行为; 公共语言运行时自动提供正确的行为。

<xref:System.Boolean>数据类型在非托管代码中具有多个表示形式。 如果未指定，则<xref:System.Boolean>数据类型的默认封送处理行为是<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 这是一个32位整数，在所有情况下均不适用。 应确定非托管方法所需的布尔表示形式，并将其与相应<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>的匹配。 Unmanagedtype.bool 是 Win32 BOOL 类型，始终为4字节。 Unmanagedtype.bool 应用于C++ `bool`或其他1字节类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突， <xref:System.Runtime.InteropServices.MarshalAsAttribute>请将<xref:System.Boolean>应用于参数或返回值。 将属性的值设置为相应<xref:System.Runtime.InteropServices.UnmanagedType>的。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 即使默认封送行为合适，也可以更轻松地在显式指定行为时维护代码。

## <a name="example"></a>示例

下面的示例演示了用适当<xref:System.Runtime.InteropServices.MarshalAsAttribute>的特性标记的平台调用方法。

[!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../code-quality/codesnippet/CSharp/ca1414-mark-boolean-p-invoke-arguments-with-marshalas_1.cs)]
[!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../code-quality/codesnippet/VisualBasic/ca1414-mark-boolean-p-invoke-arguments-with-marshalas_1.vb)]
[!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../code-quality/codesnippet/CPP/ca1414-mark-boolean-p-invoke-arguments-with-marshalas_1.cpp)]

## <a name="related-rules"></a>相关规则
[CA1901P/Invoke 声明应为可移植声明](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

[CA2101指定对 P/Invoke 字符串参数进行封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>
- [与非托管代码交互操作](/dotnet/framework/interop/index)