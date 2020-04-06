---
title: 安装可视化工作室 SDK |微软文档
ms.date: 07/12/2018
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f391708abbd8a9b66f2dfd5aaa6559cb075910d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710344"
---
# <a name="install-the-visual-studio-sdk"></a>安装 Visual Studio SDK

可视化工作室 SDK（软件开发工具包）是可视化工作室设置中的可选功能。 以后还可以安装 VS SDK。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>安装可视化工作室 SDK 作为可视化工作室安装的一部分

要将 VS SDK 包含在可视化工作室安装中，请在 **"其他工具集**"下安装**Visual Studio 扩展开发**工作负载。 此工作负载将安装可视化工作室 SDK 和必要的先决条件。 您可以通过从 **"摘要"** 视图中选择或取消选择组件来进一步调整安装。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>安装视觉工作室后安装可视化工作室 SDK

要在完成 Visual Studio 安装后安装 Visual Studio SDK，请重新运行 Visual Studio 安装程序并选择**Visual Studio 扩展开发**工作负载。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>从解决方案安装可视化工作室 SDK

如果在未首先安装 VS SDK 的情况下打开具有扩展性项目的解决方案，系统将提示**安装缺少功能对话框**以安装 Visual Studio**扩展开发**工作负荷：

![安装扩展开发](../extensibility/media/install-extension-development.png "安装扩展开发")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>从命令行安装可视化工作室 SDK

与任何 Visual Studio 工作负载或组件一样，您还可以从命令行安装**Visual Studio 扩展开发**工作负载（ID：Microsoft.VisualStudio.工作负荷.VisualStudio 扩展）。 有关适当的命令行交换机的详细信息以及有关确定工作负载或组件标识符的一般说明，请参阅[使用命令行参数安装 Visual Studio。](../install/use-command-line-parameters-to-install-visual-studio.md)

请注意，您必须使用与已安装版本的 Visual Studio 相匹配的可视化工作室安装程序。 例如，如果计算机上安装了 Visual Studio 企业版，则必须运行可视化工作室企业安装程序 *（vs_enterprise.exe*）。
