---
title: CA1403:自动布局类型不应是 COM 可见的 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5f39540cb23d86dda4244604da8a9ff764594e11
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661339"
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
 组件对象模型（COM）可见值类型标记为将 <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> 特性设置为 <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 <xref:System.Runtime.InteropServices.LayoutKind> 布局类型由公共语言运行时管理。 这些类型的布局可能在 .NET Framework 的不同版本之间更改，这会中断需要特定布局的 COM 客户端。 请注意，如果未指定 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 属性，则C#、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 和C++编译器将为值类型指定 <xref:System.Runtime.InteropServices.LayoutKind> 布局。

 除非另行标记，否则所有公共非泛型类型都对 COM 可见;所有非公共和泛型类型对 COM 都不可见。 但是，若要减少误报，此规则需要显式声明类型的 COM 可见性;必须将包含程序集标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> 设置为 `false`，并且必须将该类型标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 设置为 `true`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 特性的值更改为 <xref:System.Runtime.InteropServices.LayoutKind> 或 <xref:System.Runtime.InteropServices.LayoutKind>，或使该类型对 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型和满足规则的类型。

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/cs/FxCop.Interoperability.AutoLayout.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/vb/FxCop.Interoperability.AutoLayout.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1408：不要使用 AutoDual ClassInterfaceType ](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅
 [介绍类接口](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024) [为互操作进行互操作的 .Net 类型的符合性](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [与非托管代码进行交互操作](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
