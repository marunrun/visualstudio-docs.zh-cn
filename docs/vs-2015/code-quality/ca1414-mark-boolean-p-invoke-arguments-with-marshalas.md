---
title: CA1414：用 MarshalAs 标记布尔型 P 调用参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
helpviewer_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
ms.assetid: c0c84cf5-7701-4897-9114-66fc4b895699
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 588e16a6b21b320ad7012bd20d79a62d027679e3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652688"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414：用 MarshalAs 标记布尔型 P/Invoke 参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 平台调用方法声明包括 <xref:System.Boolean?displayProperty=fullName> 参数或返回值，但 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName> 属性不应用于参数或返回值。

## <a name="rule-description"></a>规则说明
 平台调用方法访问非托管代码，并使用 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 或 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 中的 `Declare` 关键字定义。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 指定用于在托管代码和非托管代码之间转换数据类型的封送处理行为。 许多简单的数据类型（如 <xref:System.Byte?displayProperty=fullName> 和 <xref:System.Int32?displayProperty=fullName>）在非托管代码中具有单个表示形式，并且不需要其封送行为的规范;公共语言运行时自动提供正确的行为。

 @No__t_0 的数据类型在非托管代码中具有多个表示形式。 当未指定 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 时，<xref:System.Boolean> 数据类型的默认封送处理行为 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>。 这是一个32位整数，在所有情况下均不适用。 应确定非托管方法所需的布尔表示形式，并将其与相应的 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> 匹配。 Unmanagedtype.bool 是 Win32 BOOL 类型，始终为4字节。 Unmanagedtype.bool 应该用于C++ `bool` 或其他1字节类型。 有关详细信息，请参阅[布尔类型的默认封送处理](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 应用到 <xref:System.Boolean> 参数或返回值。 将属性的值设置为相应的 <xref:System.Runtime.InteropServices.UnmanagedType>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 即使默认封送行为合适，也可以更轻松地在显式指定行为时维护代码。

## <a name="example"></a>示例
 下面的示例演示两个用适当 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性标记的平台调用方法。

 [!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cpp/FxCop.Interoperability.BoolMarshalAs.cpp#1)]
 [!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cs/FxCop.Interoperability.BoolMarshalAs.cs#1)]
 [!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/vb/FxCop.Interoperability.BoolMarshalAs.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1901：P/Invoke 声明应为可移植声明](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

 [CA2101：指定对 P/Invoke 字符串参数进行封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>请参阅
 [与非托管代码互](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)操作[的布尔类型 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> 默认封送处理](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)
