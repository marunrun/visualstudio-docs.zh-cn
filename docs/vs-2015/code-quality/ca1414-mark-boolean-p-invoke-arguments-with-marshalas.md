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
ms.openlocfilehash: 783f7fad05cad18efea2f83b6d76c4c9e644f119
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548377"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414：用 MarshalAs 标记布尔型 P/Invoke 参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|Category|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 平台调用方法声明包括 <xref:System.Boolean?displayProperty=fullName> 参数或返回值，但 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName> 特性不应用于参数或返回值。

## <a name="rule-description"></a>规则描述
 平台调用方法访问非托管代码，并通过使用 `Declare` 或中的关键字定义 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 。 <xref:System.Runtime.InteropServices.MarshalAsAttribute>指定用于在托管代码和非托管代码之间转换数据类型的封送处理行为。 许多简单的数据类型（例如 <xref:System.Byte?displayProperty=fullName> 和 <xref:System.Int32?displayProperty=fullName> ）在非托管代码中具有单个表示形式，并且不需要指定其封送处理行为; 公共语言运行时自动提供正确的行为。

 <xref:System.Boolean>数据类型在非托管代码中具有多个表示形式。 如果 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 未指定，则数据类型的默认封送处理行为 <xref:System.Boolean> 是 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> 。 这是一个32位整数，在所有情况下均不适用。 应确定非托管方法所需的布尔表示形式，并将其与相应的匹配 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> 。 Unmanagedtype.bool 是 Win32 BOOL 类型，始终为4字节。 Unmanagedtype.bool 应该用于 c + + `bool` 或其他1字节类型。 有关详细信息，请参阅[布尔类型的默认封送处理](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将应用于 <xref:System.Runtime.InteropServices.MarshalAsAttribute> <xref:System.Boolean> 参数或返回值。 将属性的值设置为相应的 <xref:System.Runtime.InteropServices.UnmanagedType> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 即使默认封送行为合适，也可以更轻松地在显式指定行为时维护代码。

## <a name="example"></a>示例
 下面的示例演示两个用适当的特性标记的平台调用方法 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 。

 [!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cpp/FxCop.Interoperability.BoolMarshalAs.cpp#1)]
 [!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cs/FxCop.Interoperability.BoolMarshalAs.cs#1)]
 [!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/vb/FxCop.Interoperability.BoolMarshalAs.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1901： P/Invoke 声明应为可移植声明](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

 [CA2101：为 P/Invoke 字符串参数指定封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>[布尔类型的默认封送处理](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)[与非托管代码互](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)操作
