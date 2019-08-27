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
ms.openlocfilehash: e0a7214ce37aa48d69b9261d686960fa0a4c308c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546344"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412:将 ComSource 接口标记为 IDispatch

|||
|-|-|
|TypeName|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因

类型将标有<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>属性和至少一个指定的接口未标有<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性设置为`InterfaceIsDispatch`值。

## <a name="rule-description"></a>规则说明

<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> 用于标识向组件对象模型 (COM) 客户端公开类的事件接口。 必须将这些接口公开为`InterfaceIsIDispatch`使 Visual Basic 6 COM 客户端可以接收事件通知。 默认情况下，如果接口未标有<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性，公开为双重接口。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请添加或修改<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性，以便其值设为使用指定的所有接口 InterfaceIsIDispatch<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示了一个接口与该规则冲突的类。

[!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../code-quality/codesnippet/CSharp/ca1412-mark-comsource-interfaces-as-idispatch_1.cs)]
[!code-vb[FxCop.Interoperability.MarkIDispatch#1](../code-quality/codesnippet/VisualBasic/ca1412-mark-comsource-interfaces-as-idispatch_1.vb)]

## <a name="related-rules"></a>相关的规则

[CA1408:不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅

- [与非托管代码交互操作](/dotnet/framework/interop/index)