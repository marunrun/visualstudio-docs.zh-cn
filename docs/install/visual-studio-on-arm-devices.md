---
title: ARM 支持的设备上的 Visual Studio
description: 在具有基于 ARM 的处理器的设备上使用 Visual Studio 的建议。
ms.date: 09/10/2020
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 367b3681d2ff8a828ee45f59359043b5fede3d26
ms.sourcegitcommit: 8a0d0f4c4910e2feb3bc7bd19e8f49629df78df5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2020
ms.locfileid: "97668100"
---
# <a name="visual-studio-on-arm-powered-devices"></a>ARM 支持的设备上的 Visual Studio

> [!IMPORTANT]
> 只有使用基于 x86 或 AMD64/x64 的处理器的设备才支持 Visual Studio。

Visual Studio 生成为基于 x86 体系结构匹配处理器，并且没有适用于基于 ARM 的处理器的 Visual Studio 版本。 但是，Windows 提供了 [ARM 上的 x86 仿真](https://www.docs.microsoft.com/windows/uwp/porting/apps-on-arm-x86-emulation)，Visual Studio 可以运行它。 通过 x86 仿真在 ARM 处理器上运行 Visual Studio 会严重影响 Visual Studio 的性能，Visual Studio 中的多项功能未设计为在这种情况下工作。 因此，建议不要在使用基于 ARM 的处理器的设备上运行 Visual Studio，而是建议使用远程目标 ARM 设备。

## <a name="remote-targeting-arm-devices"></a>远程目标 ARM 设备
为了获得最佳体验，我们建议你在 x86 支持的单独计算机上使用 Visual Studio，并使用 Visual Studio 中的远程部署和调试功能以匹配基于 ARM 的设备。 若要调试设备上已安装的 Windows 通用应用程序，请参阅[调试安装的应用包](../debugger/debug-installed-app-package.md)文档。 若要部署新应用，请参阅[远程运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。 对于所有其他应用程序类型，请参阅[远程调试](../debugger/remote-debugging.md)文档。

## <a name="tips-for-running-visual-studio-on-arm-devices"></a>在 ARM 设备上运行 Visual Studio 的提示

### <a name="use-only-when-needed"></a>仅在需要时使用
仅在特定于 ARM 的工作需要时使用 Visual Studio 优化你的时间。 任何 ARM 支持的设备的性能将要变差，你可能会发现它无法正常使用。

### <a name="install-time"></a>安装时间
计划 Visual Studio 需要更长的时间来安装，并希望暂停一段时间，或需要重新启动。
 
### <a name="remote-tools"></a>远程工具
若要调试在远程设备上运行的应用，将需要为 ARM [下载和安装远程工具](../debugger/remote-debugging.md#download-and-install-the-remote-tools)。

### <a name="start-debugging-f5"></a>启动调试 (F5)
并非所有 Visual Studio 项目都配置为从 ARM 设备开始调试 (F5) 时在本地启动项目。 即使你的应用在本地运行，也可能需要配置 Visual Studio 以进行远程调试。 有关详细信息，请参阅[远程调试](../debugger/remote-debugging.md)。

## <a name="we-need-your-help"></a>我们需要你的帮助！
如果希望 Visual Studio 在 ARM 设备上以本机方式运行，我们非常期待得到所需的方案和支持。 可以通过在[开发者社区](https://developercommunity.visualstudio.com/idea/1161018/native-arm-support-for-visual-studio.html)上发布来联系我们。
