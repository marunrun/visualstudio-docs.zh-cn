---
title: CA1412:将 ComSource 接口标记为 IDispatch
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MarkComSourceInterfacesAsIDispatch
- CA1412
helpviewer_keywords:
- CA1412
- MarkComSourceInterfacesAsIDispatch
ms.assetid: 131a7563-0410-443c-a8f5-52104250cfb4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: caaae787d5e4801f3fc3b8d881b386595fb2eca4
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234692"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412:将 ComSource 接口标记为 IDispatch

|||
|-|-|
|TypeName|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|类别|Microsoft.Interoperability|
|重大更改|重大|

## <a name="cause"></a>原因

类型使用<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>特性进行标记，且至少有一个指定接口未标记<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>为特性设置为`InterfaceIsDispatch`值。

## <a name="rule-description"></a>规则说明

<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>用于标识类向组件对象模型（COM）客户端公开的事件接口。 必须公开`InterfaceIsIDispatch`这些接口，才能使 Visual Basic 6 COM 客户端接收事件通知。 默认情况下，如果未使用<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>特性标记接口，则该接口将公开为双重接口。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>与此规则的冲突，请添加或<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>修改属性，以便将使用属性指定的所有接口的值设置为 cominterfacetype.interfaceisidispatch。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示一个类，其中其中一个接口违反规则。

[!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../code-quality/codesnippet/CSharp/ca1412-mark-comsource-interfaces-as-idispatch_1.cs)]
[!code-vb[FxCop.Interoperability.MarkIDispatch#1](../code-quality/codesnippet/VisualBasic/ca1412-mark-comsource-interfaces-as-idispatch_1.vb)]

## <a name="related-rules"></a>相关规则

[CA1408不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅

- [与非托管代码交互操作](/dotnet/framework/interop/index)