---
title: CA1408:请不要使用 AutoDual ClassInterfaceType
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotUseAutoDualClassInterfaceType
- CA1408
helpviewer_keywords:
- CA1408
- DoNotUseAutoDualClassInterfaceType
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: b26d92ca63a94cac7e293a688b1c7b3331586877
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234795"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408:请不要使用 AutoDual ClassInterfaceType

|||
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|类别|Microsoft.Interoperability|
|重大更改|重大|

## <a name="cause"></a>原因
组件对象模型（COM）可见类型被标记<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>为属性设置`AutoDual`为的值<xref:System.Runtime.InteropServices.ClassInterfaceType>。

## <a name="rule-description"></a>规则说明
使用双重接口的类型使客户端可以绑定到特定的接口布局。 如果在将来的版本中对该类型或任何基类型的布局进行更改，将中断绑定到该接口的 COM 客户端。 默认情况下，如果<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>未指定属性，则使用仅调度接口。

除非另行标记，否则所有公共非泛型类型都对 COM 可见;所有非公共和泛型类型对 COM 都不可见。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性的值更改`None`为的值<xref:System.Runtime.InteropServices.ClassInterfaceType> ，并显式定义接口。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则发出的警告，除非确定类型及其基类型的布局在未来版本中将不会更改。

## <a name="example"></a>示例
下面的示例演示一个与规则冲突的类，以及一个用于使用显式接口的类的重新声明。

[!code-csharp[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/CSharp/ca1408-do-not-use-autodual-classinterfacetype_1.cs)]
[!code-vb[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/VisualBasic/ca1408-do-not-use-autodual-classinterfacetype_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1403自动布局类型不应对 COM 可见](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

[CA1412将 ComSource 接口标记为 IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>请参阅

- [为互操作限定 .NET 类型](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [与非托管代码交互操作](/dotnet/framework/interop/index)