---
title: 安装 Visual Studio SDK |Microsoft Docs
ms.date: 07/12/2018
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4208c20cc3e7da34efaf98af16f0f41d54613824
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340759"
---
# <a name="install-the-visual-studio-sdk"></a>安装 Visual Studio SDK

Visual Studio SDK （软件开发工具包） 是在 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>作为 Visual Studio 安装的一部分安装 Visual Studio SDK

若要在 Visual Studio 安装中包括 VS SDK，安装**Visual Studio 扩展开发**下的工作负荷**其他工具集**。 此工作负荷将安装 Visual Studio SDK 和所需的先决条件。 您可以进一步优化安装，通过选中或取消选择的组件**摘要**视图。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>在安装 Visual Studio 后安装 Visual Studio SDK

若要完成你的 Visual Studio 安装后安装 Visual Studio SDK，请重新运行 Visual Studio 安装程序并选择**Visual Studio 扩展开发**工作负荷。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>从解决方案安装 Visual Studio SDK

如果不首先安装 VS SDK 与扩展性项目打开的解决方案，系统会提示通过**安装缺少的功能**对话框以安装**Visual Studio 扩展开发**工作负荷：

![安装扩展开发](../extensibility/media/install-extension-development.png "安装扩展开发")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>从命令行安装 Visual Studio SDK

如有任何 Visual Studio 工作负载或组件，还可以安装**Visual Studio 扩展开发**工作负荷 (ID:Microsoft.VisualStudio.Workload.VisualStudioExtension) 从命令行。 请参阅[使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)有关的适当的命令行开关和确定工作负荷或组件的标识符的一般说明的详细信息。

请注意，必须使用与你已安装的 Visual Studio 版本匹配的 Visual Studio 安装程序。 例如，如果必须在计算机上安装的 Visual Studio Enterprise，则必须运行 Visual Studio Enterprise 安装程序 (*vs_enterprise.exe*)。