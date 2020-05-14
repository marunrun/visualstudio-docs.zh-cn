---
title: 设置 Visual Studio for Mac Tools for Unity
description: 设置和安装用于 Visual Studio for Mac 的 Unity 工具
author: therealjohn
ms.author: johmil
ms.date: 05/25/2018
ms.assetid: 83FDD7A3-5D16-4B4B-9080-078E3FB5C623
ms.openlocfilehash: d490b4c1268beb4a5ad55263cb186d838005f718
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "79306691"
---
# <a name="set-up-visual-studio-for-mac-tools-for-unity"></a>设置 Visual Studio for Mac Tools for Unity

本部分介绍如何开始使用 Visual Studio for Mac Tools for Unity。

## <a name="install-visual-studio-for-mac"></a>安装 Visual Studio for Mac

### <a name="unity-bundled-installation"></a>Unity 捆绑安装

自 Unity 2018.1 起，Visual Studio for Mac 为 Unity 的默认 C# 集成开发环境 (IDE)，并且包含在 Unity 下载助手和 Unity 中心安装工具中。 前往 [store.unity.com](https://store.unity.com/) 下载 Unity。

在安装过程中，确保在要与 Unity 一起安装的组件列表中选中 Visual Studio for Mac：

#### <a name="unity-hub"></a>Unity Hub

![unity 中心安装](media/setup-vsmac-tools-unity-image7.png)

#### <a name="unity-download-assistant"></a>Unity 下载助手

![unity 下载助手安装](media/setup-vsmac-tools-unity-image8.png)

#### <a name="check-for-updates-to-visual-studio-for-mac"></a>检查 Visual Studio for Mac 的更新

随附于 Unity 安装的 Visual Studio for Mac 版本可能不是最新版本。 建议检查更新，确保可访问最新工具和功能。

* [更新 Visual Studio for Mac](update.md)

### <a name="manual-installation"></a>手动安装

如果已有 Unity 5.6.1 或更高版本，但没有 Visual Studio for Mac，可以手动安装 Visual Studio for Mac。 Visual Studio for Mac 的所有版本绑定 Visual Studio for Mac Tools for Unity，包括免费的 Community Edition：

* 前往 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/) 下载 Visual Studio for Mac。
* Visual Studio for Mac Tools for Unity 将在安装过程中自动安装。
* 请按照[安装指南](/visualstudio/mac/installation/?view=vsmac-2017)中的步骤获取其他安装帮助。

> [!NOTE]
> Visual Studio for Mac Tools for Unity 工具需要 5.6.1 或更高 Unity 版本。 若要验证你的 Unity 版本是否启用了 Visual Studio for Mac Tools for Unity，请从 Unity 菜单中选择“About Unity”，并在对话框左下角查看“Microsoft Visual Studio Tools for Unity 已启用”文本。 
>
> ![关于 Unity](media/setup-vsmac-tools-unity-image3.png)

## <a name="confirm-that-the-visual-studio-for-mac-tools-for-unity-extension-is-enabled"></a>确认启用 Visual Studio for Mac Tools for Unity 扩展

虽然应默认启动 Visual Studio for Mac Tools for Unity 扩展，但也可以检查安装版本号确认这一点：

1. 在 Visual Studio 菜单中，选择“Extensions...”  。

   ![选择扩展](media/setup-vsmac-tools-unity-image1.png)

2. 展开“Game Development”部分，确认 Visual Studio for Mac Tools for Unity条目。

   ![查看 Unity 条目](media/setup-vsmac-tools-unity-image2.png)

## <a name="configure-unity-for-use-with-visual-studio-for-mac"></a>配置用于 Visual Studio for Mac 的 Unity

自 Unity 2018.1 起，Visual Studio 应为 Unity 的默认外部脚本编辑器。 可以确认下是否如此，或者将外部脚本编辑器更改为 Visual Studio：

1. 从 Unity 菜单选择“Preferences...”  。

   ![选择首选项](media/setup-vsmac-tools-unity-image4.png)

2. 在“Preferences”对话框中，选择“External Tools”选项卡。 

3. 从“External Script Editor”下拉列表中，选择“Visual Studio”（如果列出此项），否则选择“Browse...”。  

   ![选择 Visual Studio](media/setup-vsmac-tools-unity-image5.png)

4. 如果已选择“Browse...”，导航到“应用程序目录”，选择“Visual Studio”，然后单击“打开”。  

   ![选择“打开”](media/setup-vsmac-tools-unity-image6.png)

5. 在“External Script Editor”列表中选择 Visual Studio 之后，关闭Preferences对话框完成配置流程。 