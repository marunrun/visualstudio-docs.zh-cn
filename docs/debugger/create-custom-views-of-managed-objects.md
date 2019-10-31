---
title: 创建托管对象的自定义视图 |Microsoft Docs
ms.date: 01/08/2019
ms.topic: conceptual
f1_keywords:
- vs.debug.data.elements
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- data types, custom
- custom data types
- managed code, custom data types
- autoexp.dat file
- mcee_cs.dat file
- debugger, expanding data types
- mcee_mc.dat file
ms.assetid: 9969e9b2-9008-4729-8a14-0d6deaa61576
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: f5247a56667f5715d9f155c662eb333967878d71
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188649"
---
# <a name="create-custom-views-of-managed-objects-c-visual-basic-f-ccli"></a>创建托管对象的自定义视图C#（、Visual Basic F#、 C++、/cli）
可以在调试器变量窗口中自定义 Visual Studio 显示数据类型的方式。

## <a name="attributes"></a>特性

在C#、Visual Basic、 F#和C++ （C++仅限/cli 代码）中，你可以使用 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>、<xref:System.Diagnostics.DebuggerDisplayAttribute> 和 <xref:System.Diagnostics.DebuggerBrowsableAttribute> 为自定义数据添加扩展。

在 .NET Framework 2.0 代码中，Visual Basic 不支持 DebuggerBrowsable 属性。 此限制已在最新版本的 .NET 中删除。

## <a name="visualizers"></a>可视化工具

可以编写可视化工具来显示任何托管数据类型。 有关详细信息，请参阅[如何：编写可视化工具](create-custom-visualizers-of-data.md)。

> [!NOTE]
> 对于C++代码，可以使用 Natvis 框架添加自定义数据类型扩展，如在[调试器中创建对象的C++自定义视图](create-custom-views-of-native-objects.md)中所述。

## <a name="see-also"></a>请参阅

- [使用 DebuggerDisplay 特性告诉调试器要显示的内容](../debugger/using-the-debuggerdisplay-attribute.md)
- [使用 DebuggerTypeProxy 特性告诉调试器要显示的类型](../debugger/using-debuggertypeproxy-attribute.md)
- [监视和快速监视窗口](../debugger/watch-and-quickwatch-windows.md)
- [使用调试器显示特性增强调试](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
