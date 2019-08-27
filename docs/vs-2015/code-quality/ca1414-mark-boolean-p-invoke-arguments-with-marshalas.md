---
title: CA1414:将布尔型 P-invoke 参数用 MarshalAs 标记 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8df0404657b6740c27544292dc101a6030a6563f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691917"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414:用 MarshalAs 标记布尔型 P/Invoke 参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 平台调用方法声明中包括<xref:System.Boolean?displayProperty=fullName>参数或返回值，但<xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName>属性不应用于参数或返回值。

## <a name="rule-description"></a>规则说明
 将平台调用方法访问非托管的代码与使用定义`Declare`中的关键字[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]或<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 指定用于托管和非托管代码之间转换数据类型的封送处理行为。 很多简单数据类型，如<xref:System.Byte?displayProperty=fullName>和<xref:System.Int32?displayProperty=fullName>、 在非托管代码中有一种表示形式和不需要其封送处理行为的规范; 公共语言运行时自动提供正确的行为。

 <xref:System.Boolean>数据类型在非托管代码中有多种表示形式。 当<xref:System.Runtime.InteropServices.MarshalAsAttribute>未指定，默认封送处理行为<xref:System.Boolean>数据类型是<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>。 这是一个 32 位整数，不是适用于所有情况。 所需的非托管方法的布尔值表示应进行确定和匹配到适当<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>。 UnmanagedType.Bool 是 Win32 BOOL 类型，它始终为 4 个字节。 应该用于 UnmanagedType.U1 C++ `bool`或其他 1 字节类型。 有关详细信息，请参阅[默认为布尔值类型封送处理](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请应用<xref:System.Runtime.InteropServices.MarshalAsAttribute>到<xref:System.Boolean>参数或返回值。 将属性的值设置为相应<xref:System.Runtime.InteropServices.UnmanagedType>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 即使是合适的默认封送处理行为，当显式指定行为更轻松地维护代码。

## <a name="example"></a>示例
 下面的示例演示两个平台调用标记有适当的方法<xref:System.Runtime.InteropServices.MarshalAsAttribute>属性。

 [!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cpp/FxCop.Interoperability.BoolMarshalAs.cpp#1)]
 [!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cs/FxCop.Interoperability.BoolMarshalAs.cs#1)]
 [!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/vb/FxCop.Interoperability.BoolMarshalAs.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1901:P/Invoke 声明应为可移植](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

 [CA2101:指定对 P/Invoke 字符串自变量封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> [默认封送处理的布尔值类型](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)[与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
