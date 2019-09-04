---
title: 开发通用 Windows 平台 (UWP) 的应用
ms.date: 10/24/2017
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: eac59cb6-f12e-4a77-9953-6d62b164a643
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 3bfe4b1a172158740705e392c573de7911016583
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70179866"
---
# <a name="develop-apps-for-the-universal-windows-platform-uwp"></a>开发通用 Windows 平台 (UWP) 的应用

使用通用 Windows 平台和我们的一项 Windows 核心，可在任何 Windows 10 设备上（从电话到桌面）运行同一应用。 使用 Visual Studio 和通用 Windows 应用开发工具创建这些通用 Windows 应用。

![通用 Windows 平台](../cross-platform/media/uwp_coreextensions.png)

在 Windows 10 手机、Windows 10 台式机或 Xbox 上运行应用。 它是相同的应用包！ 通过引入 Windows 10 的单个统一核心，一个应用程序包可以跨所有平台运行。 多个平台都具有可添加到应用以利用平台特定行为的扩展 SDK。 例如，用于移动功能的扩展 SDK 控制 Windows phone 上按下的后退按钮。 如果在项目中引用扩展 SDK，只需添加运行时检查来测试该 SDK 是否可在该平台上可用。 这就是对每个平台使用相同应用包的方法！

什么是 Windows 核心？ 

这是首次将 Windows 重构从而跨所有 Windows 10 平台共用一个核心。 存在一个共用源、一个共用 Windows 内核、一个文件 I/O 堆栈和一个应用模型。 对于 UI，只有一个 XAML UI 框架和一个 HTML UI 框架。 你可专注于创建出色的应用，因为我们已让在不同的 Windows 10 设备上运行应用变得容易。

**究竟什么是通用 Windows 平台？**

通用 Windows 平台只是一系列的协定和版本。 使你能够定位应用运行的环境。 你面向的不再是操作系统；现在你面向的是一个或多个设备系列。 请参阅[通用 Windows 平台简介](/windows/uwp/get-started/universal-application-platform-guide)，了解详细信息。

## <a name="requirements"></a>要求

通用 Windows 应用开发工具附带了仿真程序，可用于查看应用在不同设备上的显示效果。 如果想要使用这些仿真程序，需要在物理计算机上安装此软件。 物理计算机必须运行 Windows 8.1 (x64) Professional 版本或更高版本，并具有支持客户端 Hyper-V 和二级地址转换 (SLAT) 的处理器。 当 Visual Studio 安装在虚拟机上时，则无法使用仿真程序。

下面是所需软件的列表：

::: moniker range="vs-2017"

- [Windows 10](http://windows.microsoft.com/windows/downloads)。 Visual Studio 2017 只在 Windows 10 上支持 UWP 开发。 有关详细信息，请参阅 Visual Studio [平台目标](/visualstudio/productinfo/vs2017-compatibility-vs)和[系统要求](/visualstudio/productinfo/vs2017-system-requirements-vs)。

- [Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)。 你还需要通用 Windows 平台开发工作负荷（可选）。

     ![UWP 工作负荷](media/uwp_workload.png)

::: moniker-end

::: moniker range="vs-2019"

- [Windows 10](http://windows.microsoft.com/windows/downloads)。 Visual Studio 2019 只在 Windows 10 上支持 UWP 开发。 有关详细信息，请参阅 Visual Studio [平台目标](/visualstudio/releases/2019/compatibility/)和[系统要求](/visualstudio/releases/2019/system-requirements/)。

- [Visual Studio](https://visualstudio.microsoft.com/downloads)。 你还需要通用 Windows 平台开发工作负荷（可选）。

     ![UWP 工作负荷](media/uwp_workload.png)

::: moniker-end

安装此软件后，需要启用 Windows 10 设备以进行开发。 请参阅[启用设备进行开发](/windows/uwp/get-started/enable-your-device-for-development)。 不再需要每个 Windows 10 设备的开发者许可证。

## <a name="universal-windows-apps"></a>通用 Windows 应用

从 C#、Visual Basic、C++ 或 JavaScript 中选择首选的开发语言用来为 Windows 10 设备创建通用 Windows 平台应用。 请参阅[创建你的第一个应用](/windows/uwp/get-started/your-first-app)或观看 [Tools for Windows 10 Overview](https://channel9.msdn.com/Series/ConnectOn-Demand/229)（Windows 10 工具概述）视频。

如果你目前已有通过 Visual Studio 2015 创建的 Windows 应用商店 8.1 应用、Windows Phone 8.1 应用或通用 Windows 应用，则需移植这些应用，以使用最新的通用 Windows 平台。 请参阅[从 Windows 运行时 8.x 移动到 UWP](/windows/uwp/porting/w8x-to-uwp-root)。

创建通用 Windows 应用后，必须将应用打包，以将其安装在 Windows 10 设备上或提交到 Windows 应用商店。 请参阅[打包应用](/windows/uwp/packaging/index)。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的跨平台移动开发](../cross-platform/cross-platform-mobile-development-in-visual-studio.md)
