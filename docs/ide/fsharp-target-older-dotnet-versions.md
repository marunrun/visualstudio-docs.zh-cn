---
title: 针对 F# 面向旧版 .NET Framework
description: 了解在 Visual Studio 中使用 F# 时如何面向 .NET Framework 的较旧版本。
ms.date: 07/11/2018
ms.topic: troubleshooting
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
monikerRange: vs-2017
ms.openlocfilehash: df263ee4b2bd6ec7b6239826725a85c26f0acf80
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603531"
---
# <a name="target-older-versions-of-net-f"></a>面向 .NET 的较旧版本 (F#)

在 Windows 8.1 上安装 Visual Studio 后，如果尝试在 F# 项目中面向 .NET Framework 2.0、3.0 或 3.5，则可能出现以下错误：

此项目需要 2.0 F# 运行时，但该运行时未安装。 

已知同时满足以下条件时会出现此错误：

- 已在 Windows 8.1 上安装 Visual Studio。

- 未在安装 Visual Studio 之前启用 .NET Framework 3.5。

- 项目面向 .NET Framework 2.0、3.0 或 3.5。

安装 Visual Studio 时，它会检测已安装的 .NET Framework 版本。 Visual Studio 仅在已安装并启用 .NET Framework 3.5 时才安装 F# 2.0 运行时。

## <a name="resolve-the-error"></a>解决错误

可通过以下任一方法解决该错误：

- 面向 .NET Framework 的较新版本。

- 在 Windows 8.1 上启用 .NET Framework 3.5，然后通过修复 Visual Studio 安装来安装 F# 2.0 运行时。 操作步骤如下。

### <a name="to-enable-the-net-framework-35-on-windows-81"></a>在 Windows 8.1 上启用 .NET Framework 3.5

1. 在“开始”屏幕上，键入“控制面板”   。

   键入时，“应用”标题下将出现“控制面板”图标   。

2. 选择“控制面板”图标，选择“程序”图标，然后选择“打开或关闭 Windows 功能”链接    。

3. 请确保选中“.NET Framework 3.5 (包括 .NET 2.0 和 3.0)”复选框，然后选择“确定”按钮   。 不需要选择 .NET framework 可选组件的任何子节点对应的复选框。

   .NET Framework 3.5 随即启用（如果尚未启用）。

### <a name="to-install-the-f-20-runtime"></a>安装 F# 2.0 运行时

请按照[修复 Visual Studio 的步骤](../install/repair-visual-studio.md)执行操作。

## <a name="see-also"></a>请参阅

- [F# 指南 (.NET Framework)](/dotnet/fsharp/)
- [Visual Studio 中的 F#](fsharp-visual-studio.md)