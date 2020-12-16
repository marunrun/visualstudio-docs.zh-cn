---
title: 安装 Visual Studio SDK | Microsoft Docs
description: 了解 Visual Studio 软件开发工具包的安装选项，包括在 Visual Studio 安装期间。
ms.custom: SEO-VS-2020
ms.date: 07/12/2018
ms.topic: overview
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: edab24396f5a3ae5527b76a58db90c19796c4240
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487564"
---
# <a name="install-the-visual-studio-sdk"></a>安装 Visual Studio SDK

Visual Studio SDK（软件开发工具包）是 Visual Studio 安装程序中的一个可选功能。 也可稍后安装 VS SDK。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>在安装 Visual Studio 的过程中安装 Visual Studio SDK

要在安装 Visual Studio 时安装 VS SDK，请安装“其他工具集”下的“Visual Studio 扩展开发”工作负载 。 此工作负载将安装 Visual Studio SDK 和所需必备组件。 可以通过从“摘要”视图中选择或取消选择组件来进一步优化安装。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>在安装 Visual Studio 后安装 Visual Studio SDK

要在完成 Visual Studio 安装后安装 Visual Studio SDK，请重新运行 Visual Studio 安装程序，并选择“Visual Studio 扩展开发”工作负载。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>从解决方案安装 Visual Studio SDK

如果在未先安装 VS SDK 的情况下打开包含扩展性项目的解决方案，则会出现“安装缺少的功能”对话框，提示安装“Visual Studio 扩展开发”工作负载 ：

![安装扩展开发](../extensibility/media/install-extension-development.png "安装扩展开发")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>从命令行安装 Visual Studio SDK

对于任何 Visual Studio 工作负载或组件，还可以从命令行安装“Visual Studio 扩展开发”工作负载（ID：Microsoft.VisualStudio.Workload.VisualStudioExtension）。 请参阅[使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)，获取有关适当的命令行开关的详细信息和有关确定工作负载或组件标识符的一般说明。

请注意，必须使用与已安装的 Visual Studio 版本匹配的 Visual Studio 安装程序。 例如，如果计算机上安装了 Visual Studio Enterprise，则必须运行 Visual Studio Enterprise 安装程序 (vs_enterprise.exe)。
