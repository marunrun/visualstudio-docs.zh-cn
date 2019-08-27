---
title: 互操作性警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis warnings, interoperability warnings
- interoperability warnings
- warnings, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7a4e8f7bc60704842a8a0e940b336b4bb79093b2
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66745133"
---
# <a name="interoperability-warnings"></a>互操作性警告

互操作性警告支持与 COM 客户端进行交互。

## <a name="in-this-section"></a>本节内容

| 规则 | 描述 |
| - | - |
| [CA1400:P/Invoke 入口点应该存在](../code-quality/ca1400-p-invoke-entry-points-should-exist.md) | 公共或受保护方法标有 System.Runtime.InteropServices.DllImportAttribute 特性。 未能找到非托管库，或者未能将方法与库中的函数匹配。 |
| [CA1401:P/Invokes 应该是不可见](../code-quality/ca1401-p-invokes-should-not-be-visible.md) | 中的公共类型的公共或受保护方法具有 System.Runtime.InteropServices.DllImportAttribute 特性 （还通过在 Visual Basic 中的 Declare 关键字实现）。 这些方法不能公开。 |
| [CA1402:避免在 COM 可见接口中的重载](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md) | 在向 COM 客户端公开重载的方法时，只有第一个方法重载保留其名称。 对于后续重载，将为其指定唯一名称，方法是在其名称后面追加一个下划线字符 (_) 和一个与该重载的声明顺序对应的整数。 |
| [CA1403:自动布局类型不应对 COM 可见](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md) | 某个 COM 可见的值类型用设置为 LayoutKind.Auto 的 System.Runtime.InteropServices.StructLayoutAttribute 特性标记。这些类型的布局可以将中断要求特定布局的 COM 客户端的.NET 版本之间进行更改。 |
| [CA1404:紧接在 P/Invoke 之后调用 GetLastError](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md) | 调用了 Marshal.GetLastWin32Error 方法或等效[!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)]GetLastError 函数，并紧位于前面的调用不到的平台调用方法。 |
| [CA1405:COM 可见类型的基类型应对 COM 可见](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md) | 某个 COM 可见的类型是从非 COM 可见的类型派生而来。 |
| [CA1406:避免对 Visual Basic 6 客户端的 Int64 参数](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md) | Visual Basic 6 COM 客户端不能访问 64 位整数。 |
| [CA1407:避免在 COM 可见类型中的静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md) | COM 不支持静态方法。 |
| [CA1408:不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md) | 使用双重接口的类型使客户端可以绑定到特定的接口布局。 如果在将来的版本中对该类型或任何基类型的布局进行更改，将中断绑定到该接口的 COM 客户端。 默认情况下，如果未指定 ClassInterfaceAttribute 特性，则使用仅支持调度的接口。 |
| [CA1409:Com 可见类型应该是可创建对象](../code-quality/ca1409-com-visible-types-should-be-creatable.md) | 专门标记为对 COM 可见的某个引用类型包含公共的参数化构造函数，但不包含公共的默认（无参数）构造函数。 没有公共默认构造函数的类型不能由 COM 客户端创建。 |
| [CA1410:应对 COM 注册方法进行匹配](../code-quality/ca1410-com-registration-methods-should-be-matched.md) | 某个类型声明的方法，使用标记<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>属性，但不声明使用标记的方法<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>属性，反之亦然。 |
| [CA1411:COM 注册方法应该是不可见](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md) | 通过用 System.Runtime.InteropServices.ComRegisterFunctionAttribute 特性或 System.Runtime.InteropServices.ComUnregisterFunctionAttribute 特性标记的方法是外部可见的。 |
| [CA1412:将 ComSource 接口标记为 IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md) | 某个类型用 System.Runtime.InteropServices.ComSourceInterfacesAttribute 特性标记，并且至少一个指定的接口未用设置为 ComInterfaceType.InterfaceIsIDispatch 的 System.Runtime.InteropServices.InterfaceTypeAttribute 特性标记。 |
| [CA1413:避免在 COM 可见值类型中的非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md) | 对 COM 可见的值类型的非公共实例字段对 COM 客户端可见。 请检查各个字段的内容以查找不应当公开的信息或将对设计或安全性造成意外影响的信息。 |
| [CA1414:标记用 MarshalAs 布尔型 P/Invoke 参数](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md) | Boolean 数据类型在非托管代码中有多种表示形式。 |
| [CA1415:正确声明 P/Invoke](../code-quality/ca1415-declare-p-invokes-correctly.md) | 此规则查找针对平台调用方法声明面向[!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)]函数具有指向 OVERLAPPED 结构参数和对应的托管的参数不是一个指向<xref:System.Threading.NativeOverlapped?displayProperty=fullName>结构。 |