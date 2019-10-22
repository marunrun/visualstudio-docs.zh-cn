---
title: 开发面向通用 Windows 平台 (UWP) 的应用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: eac59cb6-f12e-4a77-9953-6d62b164a643
caps.latest.revision: 50
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ed601f6b3bfeba4d7aebed5955b340fb28908c74
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660204"
---
# <a name="develop-apps-for-the-universal-windows-platform-uwp"></a>开发通用 Windows 平台 (UWP) 的应用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用通用 Windows 平台和我们的一项 Windows 核心，可在任何 Windows 10 设备上（从电话到桌面）运行同一应用。 使用 Visual Studio 2015 和通用 Windows 应用开发工具创建这些通用 Windows 应用。

 ![通用 Windows 平台](../cross-platform/media/uwp-coreextensions.png "UWP_CoreExtensions")

 在 Windows 10 手机、Windows 10 台式机或 Xbox 上运行应用。 它是相同的应用程序包！ 通过引入 Windows 10 的单个统一核心，一个应用程序包可以跨所有平台运行。 多个平台都具有可添加到应用以利用平台特定行为的扩展 SDK。 例如，用于移动功能的扩展 SDK 控制 Windows phone 上按下的后退按钮。 如果在项目中引用扩展 SDK，只需添加运行时检查来测试该 SDK 是否可在该平台上可用。 这就是对每个平台使用相同应用程序包的方法了！

 **什么是 Windows 核心？**

 这是首次将 Windows 重构从而跨所有 Windows 10 平台共用一个核心。 存在一个共用源、一个共用 Windows 内核、一个文件 I/O 堆栈和一个应用模型。 对于 UI，只有一个 XAML UI 框架和一个 HTML UI 框架。 因此你可专注于创建出色的应用，因为我们已让在不同的 Windows 10 设备上运行应用变得容易。

 **究竟什么是通用 Windows 平台？**

 它只是一个协定和版本的集合。 使你能够定位应用运行的环境。 不用再定位到操作系统。 现在你可以将应用定位到一个或多个设备系列。 通过此 [平台指南](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx)了解更多详细信息。

## <a name="requirements"></a>要求
 通用 Windows 应用开发工具附带了仿真程序，可用于查看应用在不同设备上的显示效果。 如果想要使用这些仿真程序，需要在物理计算机上安装此软件。 物理计算机必须运行 Windows 8.1 (x64) Professional 版本或更高版本，并具有支持客户端 Hyper-V 和二级地址转换 (SLAT) 的处理器。 当 Visual Studio 安装在虚拟机上时，则无法使用仿真程序。

 下面是所需软件的列表：

- [Windows 10](http://windows.microsoft.com/windows/downloads)

- [Visual Studio 2015](http://go.microsoft.com/fwlink/p/?LinkId=526725)。 请确保可选功能列表中，通用 Windows 应用开发工具处于选中状态。 没有这些工具，你将无法创建通用应用。

  在安装此软件之后，你需要 [启用 Windows 10 设备](https://msdn.microsoft.com/library/windows/apps/xaml/dn706236.aspx) 以进行开发。 （不再需要每个 Windows 10 设备的开发人员许可证。）

  **Windows 8.1 和 Windows 7 支持**

  如果选择使用 Visual Studio 2015 在除 Windows 10 外的平台上开发通用 Windows 应用，存在以下限制：

- Windows 8.1：不能在本地运行应用（仅在远程 Windows 10 设备上运行）。 可使用 Visual Studio 中的仿真程序，但不能使用模拟器。

- Windows 7：不能在本地运行应用（仅在远程 Windows 10 设备上运行）。 不能使用 Visual Studio 中的仿真程序或模拟器。

  如果开发平台是 Windows 10，只能使用 XAML 设计器。

## <a name="universal-windows-apps"></a>通用 Windows 应用
 从 C#、Visual Basic、C++ 或 JavaScript 中选择首选的开发语言以 [为 Windows 10 设备创建通用 Windows 应用](https://msdn.microsoft.com/library/windows/apps/xaml/dn609832.aspx#target_win10)。 或者，监视 [此入门视频](http://channel9.msdn.com/Series/ConnectOn-Demand/229)。

 如果你有现有的 Windows 应用商店 8.1 应用、Windows Phone 8.1 应用或使用 Visual Studio 2015 RC 创建的通用 Windows 应用，则 [移植这些现有的应用](https://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) 以使用最新的通用 Windows 平台。

 创建通用 Windows 应用后，必须 [将应用打包](https://msdn.microsoft.com/library/windows/apps/hh454036.aspx) 以将其安装在 Windows 10 设备或提交到 Windows 应用商店。
