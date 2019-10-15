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
ms.openlocfilehash: 4e590514247444d32d0d9a31b2bbc409434cf53c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234825"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403:自动布局类型不应对 COM 可见

|||
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|类别|Microsoft.Interoperability|
|重大更改|重大|

## <a name="cause"></a>原因

组件对象模型（COM）可见值类型标记<xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName>为属性设置为。 <xref:System.Runtime.InteropServices.LayoutKind.Auto?displayProperty=fullName>

## <a name="rule-description"></a>规则说明

<xref:System.Runtime.InteropServices.LayoutKind>布局类型由公共语言运行时管理。 这些类型的布局可能在 .NET 版本之间更改，这会中断需要特定布局的 COM 客户端。 如果未指定 <xref:System.Runtime.InteropServices.StructLayoutAttribute>C# C++ 属性，则、Visual Basic 和编译器会为值类型指定 [LayoutKind.Auto](<xref:System.Runtime.InteropServices.LayoutKind.Auto>)

除非另行标记，否则所有公共、非泛型类型都对 COM 可见，所有非公共和泛型类型对 COM 都不可见。 但是，若要减少误报，此规则需要显式声明类型的 COM 可见性。 必须用<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>设置为`false`的将包含程序集标记为，且类型<xref:System.Runtime.InteropServices.ComVisibleAttribute>必须`true`标记为。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请将<xref:System.Runtime.InteropServices.StructLayoutAttribute>属性的值更改为[LayoutKind](<xref:System.Runtime.InteropServices.LayoutKind.Explicit>)或[LayoutKind](<xref:System.Runtime.InteropServices.LayoutKind.Sequential>)，或使该类型对 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示违反规则的类型和满足规则的类型。

[!code-csharp[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/CSharp/ca1403-auto-layout-types-should-not-be-com-visible_1.cs)]
[!code-vb[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/VisualBasic/ca1403-auto-layout-types-should-not-be-com-visible_1.vb)]

## <a name="related-rules"></a>相关规则

[CA1408不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅

- [为互操作限定 .NET 类型](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [与非托管代码交互操作](/dotnet/framework/interop/index)