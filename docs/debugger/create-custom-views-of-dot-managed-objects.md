---
title: 创建对象的自定义视图 |Microsoft Docs
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
ms.openlocfilehash: 911f0423184f22919be016691b9333b2f62d1b61
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744789"
---
# <a name="create-custom-views-of-objects-c-visual-basic-c"></a>创建自定义视图的对象 (C#，Visual Basic 中， C++)
可以在调试器变量窗口中自定义 Visual Studio 显示数据类型的方式。

## <a name="native-code"></a>本机代码

有关C++代码中，您可以添加自定义数据类型扩展使用 Natvis 框架，如中所述[创建自定义视图的C++在调试器中的对象](/visualstudio/debugger/create-custom-views-of-native-objects)。 有关C++/CLI 代码中，您还可以使用本文中的此处所述的特性。

## <a name="attributes"></a>特性

在C#，Visual Basic 和C++(C++仅 /CLI 代码)，可以添加自定义数据使用的扩展<xref:System.Diagnostics.DebuggerTypeProxyAttribute>， <xref:System.Diagnostics.DebuggerDisplayAttribute>，和<xref:System.Diagnostics.DebuggerBrowsableAttribute>。

在.NET Framework 2.0 代码中，Visual Basic 不支持 DebuggerBrowsable 特性。 此项限制在 .NET Framework 较高版本中已经删除。

## <a name="visualizers"></a>可视化工具

可以编写可视化工具来显示任何托管数据类型。 有关详细信息，请参阅[如何：编写可视化工具](/visualstudio/debugger/create-custom-visualizers-of-data)。

## <a name="see-also"></a>请参阅

- [让调试程序要演示如何使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)
- [让调试器在哪种类型来演示如何使用 DebuggerTypeProxy 特性](../debugger/using-debuggertypeproxy-attribute.md)
- [监视和快速监视窗口](../debugger/watch-and-quickwatch-windows.md)
- [使用调试器显示特性增强调试](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)