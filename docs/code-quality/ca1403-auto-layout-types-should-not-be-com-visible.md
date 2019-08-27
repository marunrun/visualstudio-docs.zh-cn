---
title: CA1403:自动布局类型不应对 COM 可见
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: ef7b693a881aaa1457004c84968ebc80936fc2b2
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714849"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403:自动布局类型不应对 COM 可见

|||
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因

组件对象模型 (COM) 可见值类型将标有<xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName>属性设置为<xref:System.Runtime.InteropServices.LayoutKind.Auto?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明

<xref:System.Runtime.InteropServices.LayoutKind> 由公共语言运行时管理布局类型。 这些类型的布局可以更改.NET，这将中断要求特定布局的 COM 客户端的不同版本之间。 如果<xref:System.Runtime.InteropServices.StructLayoutAttribute>未指定属性， C#，Visual Basic 中，和C++编译器指定[LayoutKind.Auto](<xref:System.Runtime.InteropServices.LayoutKind.Auto>)对于值类型。

除非以其他方式标记，所有公共、 非泛型类型对于 COM 可见，且所有的非公共和泛型类型对 COM 不可见 但是，若要减少误报，此规则要求显式声明的类型的 COM 可见性。 包含程序集必须使用标记<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>设置为`false`和类型必须标有<xref:System.Runtime.InteropServices.ComVisibleAttribute>设置为`true`。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请更改的值<xref:System.Runtime.InteropServices.StructLayoutAttribute>归于[LayoutKind.Explicit](<xref:System.Runtime.InteropServices.LayoutKind.Explicit>)或[LayoutKind.Sequential](<xref:System.Runtime.InteropServices.LayoutKind.Sequential>)，或使类型对 COM 不可见

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示了违反规则的类型，并满足该规则的类型。

[!code-csharp[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/CSharp/ca1403-auto-layout-types-should-not-be-com-visible_1.cs)]
[!code-vb[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/VisualBasic/ca1403-auto-layout-types-should-not-be-com-visible_1.vb)]

## <a name="related-rules"></a>相关的规则

[CA1408:不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅

- [限定.NET 类型的互操作](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [与非托管代码进行互操作](/dotnet/framework/interop/index)