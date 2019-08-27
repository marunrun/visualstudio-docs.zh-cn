---
title: CA1403:自动布局类型不应对 COM 可见 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 2420582ab342948d7774e1bb9e4b5947f44f8d2b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695442"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403:自动布局类型不应对 COM 可见
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 组件对象模型 (COM) 可见值类型将标有<xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName>属性设置为<xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 <xref:System.Runtime.InteropServices.LayoutKind> 由公共语言运行时管理布局类型。 这些类型的布局可以更改.NET Framework 中，将中断要求特定布局的 COM 客户端的不同版本之间。 请注意，如果<xref:System.Runtime.InteropServices.StructLayoutAttribute>未指定属性， C#， [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，并C++编译器指定<xref:System.Runtime.InteropServices.LayoutKind>对于值类型的布局。

 除非以其他方式标记，所有公共的非泛型类型都是对 COM 可见所有非公共和泛型类型是对 COM 不可见 但是，若要减少误报，此规则要求类型来显式声明; COM 可见的性包含程序集必须使用标记<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>设置为`false`和类型必须标有<xref:System.Runtime.InteropServices.ComVisibleAttribute>设置为`true`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改的值<xref:System.Runtime.InteropServices.StructLayoutAttribute>归于<xref:System.Runtime.InteropServices.LayoutKind>或<xref:System.Runtime.InteropServices.LayoutKind>，或使类型对 COM 不可见

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了违反规则的类型，并满足该规则的类型。

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/cs/FxCop.Interoperability.AutoLayout.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/vb/FxCop.Interoperability.AutoLayout.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1408:不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅
 [类接口简介](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[为互操作限定.NET 类型](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
