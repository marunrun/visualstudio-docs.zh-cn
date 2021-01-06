---
title: Visual Studio Tools for Unity 入门 | Microsoft Docs
description: 了解如何安装和设置 Visual Studio for Unity 开发。
ms.custom: ''
ms.date: 07/13/2020
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 1f8cbe1629aab6a177a46888fe25cf8e3565d91d
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903748"
---
# <a name="get-started-with-visual-studio-and-unity"></a>Visual Studio 和 Unity 入门

> [!NOTE]
> 本指南假定你已使用 Unity 中心程序安装了 Unity。 如果你不熟悉 Unity，我们建议先访问 Unity 了解并 [通过 unity 教程完成入门](https://learn.unity.com/course/getting-started-with-unity) 。

## <a name="install-unity-support-for-visual-studio"></a>安装适用于 Visual Studio 的 Unity 支持

Visual Studio Tools for Unity 是一种免费扩展，它为编写和调试 c # 等提供支持。 有关扩展所包含内容的完整列表，请访问 [适用于 Unity 的工具概述](./visual-studio-tools-for-unity.md) 。

:::zone pivot="windows"

> [!NOTE]
> 本安装指南适用于 Visual Studio。 如果你正在使用 Visual Studio Code，请 [使用 VS Code 文档访问 Unity 开发](https://code.visualstudio.com/docs/other/unity)。

1. [下载 Visual Studio 安装程序](/visualstudio/docs/install/install-visual-studio.md)，或者在已安装的情况下运行它。
2. 为所需的 Visual Studio 版本单击“修改”（如已安装）或“安装”（适用于新安装）。
3. 在 " **工作负荷** " 选项卡上，滚动到 " **游戏** " 部分，选择 " **包含 Unity 的游戏开发** " 工作负荷。

    ![安装程序中的 "通过 Unity 工作负荷进行游戏开发"](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> 本安装指南适用于 Visual Studio for Mac。 如果你正在使用 Visual Studio Code，请 [使用 VS Code 文档访问 Unity 开发](https://code.visualstudio.com/docs/other/unity)。

适用于 Unity 的工具包含在 Visual Studio for Mac 安装中，无需单独安装步骤。 可以在 **Visual Studio for Mac > 扩展 > 游戏开发** "菜单中对此进行验证。 应启用 **Unity Visual Studio for Mac 工具**。

![显示已启用 Unity Visual Studio for Mac 工具的 "扩展管理器" 视图](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>检查更新

建议将 Visual Studio 和 Visual Studio for Mac 更新，以便获得最新的 bug 修复、功能和 Unity 支持。 这不需要更新 Unity 版本。

:::zone pivot="windows"

1. 单击 " **帮助" > "检查更新** " 菜单。

    ![Visual Studio 2019 中的 "检查更新" 菜单](../media/vs/check-for-updates.png)

2. 如果有可用的更新，则 Visual Studio 安装程序将显示新版本。 单击“更新”按钮。

:::zone-end
:::zone pivot="macos"

1. 单击 " **Visual Studio for Mac > 检查更新 ...** " 菜单以打开 " **Visual Studio 更新** " 对话框。
2. 如果有可用的更新，请单击 " **安装** " 按钮。

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>将 Unity 配置为使用 Visual Studio

默认情况下，Unity 应已配置为使用 Visual Studio 或 Visual Studio for Mac 作为脚本编辑器。 可以通过 Unity 编辑器确认这一点，或将外部脚本编辑器更改为 Visual Studio 的特定版本。

:::zone pivot="windows"

1. 在 Unity 编辑器中，选择 " **编辑 > 首选项** " 菜单。
2. 选择左侧的 " **外部工具** " 选项卡。
3. " **外部脚本编辑器** " 下拉列表提供了一种选择不同的 Visual Studio 安装的方法。 还可以从下拉列表中单击 " **浏览 ...** " 以添加未列出的版本。

    ![Windows 上 Unity 编辑器中的 "外部工具" 首选项菜单](../media/vs/preferences-external-tools.png)

4. 如果已选择 **Browse...** ，请导航到 Visual Studio 安装目录中的 **Common7/IDE** 目录，然后选择 **devenv.exe**。 然后单击 " **打开**"。
5. 在 **External Script Editor** 列表中选择 Visual Studio 后，确认已选中 **Editor Attaching** 复选框。
6. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end
:::zone pivot="macos"

1. 在 Unity 编辑器中，选择 " **unity > 首选项** " 菜单。
2. 选择左侧的 " **外部工具** " 选项卡。
3. " **外部脚本编辑器** " 下拉列表提供了一种选择不同的 Visual Studio 安装的方法。 还可以从下拉列表中单击 " **浏览 ...** " 以添加未列出的版本。

    ![MacOS 上 Unity 编辑器中的 "外部工具" 首选项菜单](../media/vsm/preferences-external-tools.png)

4. 关闭 **Preferences** 对话框以完成配置过程。

:::zone-end

## <a name="next-steps"></a>后续步骤

 若要了解如何在 Visual Studio 中使用和调试 Unity 项目，请参阅 [使用 Visual Studio Tools for Unity](using-visual-studio-tools-for-unity.md)。
