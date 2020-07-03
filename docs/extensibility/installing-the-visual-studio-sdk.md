---
title: 安装 Visual Studio SDK |Microsoft Docs
ms.date: 07/12/2018
ms.topic: overview
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31df92b011336320d759461ed16ce2a3c8f61017
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905544"
---
# <a name="install-the-visual-studio-sdk"></a>安装 Visual Studio SDK

Visual Studio SDK （软件开发工具包）是 Visual Studio 安装程序中的一项可选功能。 你还可以在以后安装 VS SDK。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>安装 visual Studio SDK 作为 Visual Studio 安装的一部分

若要在 Visual Studio 安装中包含 VS SDK，请在 "**其他工具集**" 下安装**visual studio 扩展开发**工作负荷。 此工作负荷将安装 Visual Studio SDK 和必要的必备组件。 可以通过从 "**摘要**" 视图中选择或取消选择组件来进一步优化安装。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>安装 Visual Studio 后安装 Visual Studio SDK

若要在完成 Visual Studio 安装后安装 Visual Studio SDK，请重新运行 Visual Studio 安装程序并选择 " **Visual studio 扩展开发**" 工作负荷。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>从解决方案安装 Visual Studio SDK

如果在未首先安装 VS SDK 的情况下使用扩展性项目打开解决方案，则安装**Visual Studio 扩展开发**工作负荷时，会出现 "**安装缺少的功能**" 对话框。

![安装扩展开发](../extensibility/media/install-extension-development.png "安装扩展开发")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>从命令行安装 Visual Studio SDK

对于任何 Visual Studio 工作负荷或组件，还可以从命令行安装**Visual studio 扩展开发**工作负荷（ID： VisualStudio）。 有关相应的命令行开关的详细信息，请参阅[使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)和确定工作负荷或组件标识符的一般说明。

请注意，必须使用与已安装的 Visual Studio 版本匹配的 Visual Studio 安装程序。 例如，如果您的计算机上安装了 Visual Studio Enterprise，则必须运行 Visual Studio Enterprise 安装程序（*vs_enterprise.exe*）。
