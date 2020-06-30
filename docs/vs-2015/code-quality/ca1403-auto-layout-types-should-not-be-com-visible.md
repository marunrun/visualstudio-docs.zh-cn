---
title: CA1403：自动布局类型不应是 COM 可见的 |Microsoft Docs
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
ms.openlocfilehash: 1752efb5be1828f62703e1fe1a1130b37ff80503
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534922"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403:自动布局类型不应对 COM 可见
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|Category|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 组件对象模型（COM）可见值类型标记为 <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> 属性设置为 <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 <xref:System.Runtime.InteropServices.LayoutKind>布局类型由公共语言运行时管理。 这些类型的布局可能在 .NET Framework 的不同版本之间更改，这会中断需要特定布局的 COM 客户端。 请注意，如果 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 未指定属性，则 c #、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 和 c + + 编译器将指定 <xref:System.Runtime.InteropServices.LayoutKind> 值类型的布局。

 除非另行标记，否则所有公共非泛型类型都对 COM 可见;所有非公共和泛型类型对 COM 都不可见。 但是，若要减少误报，此规则需要显式声明类型的 COM 可见性;必须用设置为的将包含程序集标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> `false` ，且类型必须标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute> `true` 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将属性的值更改 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 为 <xref:System.Runtime.InteropServices.LayoutKind> 或 <xref:System.Runtime.InteropServices.LayoutKind> ，或使该类型对 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型和满足规则的类型。

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/cs/FxCop.Interoperability.AutoLayout.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/vb/FxCop.Interoperability.AutoLayout.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1408:请不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>另请参阅
 [介绍类接口](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[为互操作进行互操作的 .Net 类型的符合](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [Interoperating with Unmanaged Code](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)性
