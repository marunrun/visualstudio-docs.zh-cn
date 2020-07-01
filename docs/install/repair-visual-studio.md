---
title: 修复 Visual Studio
titleSuffix: ''
description: 了解如何修复 Visual Studio 2017 的安装
ms.date: 06/15/2020
ms.custom: seodec18
ms.topic: how-to
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: fda72206059e5c14c46d332e44ea0de481004296
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418959"
---
# <a name="repair-visual-studio"></a>修复 Visual Studio

Visual Studio 安装有时会损毁或损坏。 修复对于修复所有安装操作（包括更新）中的安装时问题非常有用。

## <a name="when-to-use-repair"></a>何时使用修复
* 如果遇到安装有效负载问题。 当无法将文件写入到磁盘，且无法通过删除损坏的文件来修复时，可能会发生这种情况。 修复可以重新获取所需的文件。 
* 如果遇到客户端下载问题。 修复可能会有所帮助的前提是，已解决任何连接或代理问题。 
* 如果在更新 Visual Studio 时遇到问题。 修复可解决许多常见的更新问题。 

> [!TIP] 
> 如果安装问题是由基础 Windows 服务（如 Windows Installer）中的问题引起的，则修复可能会遇到相同的问题。 系统问题可能包括，损坏的 Windows Installer ，或不稳定的 Internet 连接。 若要检查是否有系统问题，请使用通过安装操作生成的错误报告。

> [!NOTE] 
> 修复 Visual Studio 会重置用户设置，并重新安装已有的程序集。 如果遇到产品问题，请创建 [Visual Studio 反馈票证](https://developercommunity.visualstudio.com/content/problem/post.html?space=8)，因为修复可能无法解决此问题。

## <a name="how-to-repair"></a>如何修复
::: moniker range="vs-2017"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 周年更新或更高版本的计算机上，选择“开始”，再滚动到字母“V”（其中它被列为“Visual Studio 安装程序”）。

   > [!NOTE]
   > 对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。
   >
   > 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 打开安装程序，选择“更多”，然后选择“修复”。

    ![从 Visual Studio 安装程序修复 Visual Studio](media/repair-visual-studio.png "从 Visual Studio 安装程序修复 Visual Studio")

   > [!NOTE]
   > 修复 Visual Studio 将重置环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 将还原主题、颜色、键绑定等同步设置。
   >

   > [!TIP]
   > “修复”选项仅对已安装的 Visual Studio 实例显示。 如果没有看到“修复”选项，很可能是因为选择“更多”时所在的版本在 Visual Studio 安装程序中列为“可用”，而不是“已安装”。

::: moniker-end

::: moniker range="vs-2019"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出  。

     ![打开 Visual Studio 安装程序](media/vs-2019/vs-installer-windows-start.png "打开 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本。 接下来，选择“更多”，然后选择“修复”。

     ![修复 Visual Studio 2019](media/vs-2019/vs-installer-repair.png "修复 Visual Studio 2019")

   > [!NOTE]
   > 修复 Visual Studio 将重置环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 将还原主题、颜色、键绑定等同步设置。
   >

   > [!TIP]
   > “修复”选项仅对已安装的 Visual Studio 实例显示。 如果没有看到“修复”选项，很可能是因为选择“更多”时所在的版本在 Visual Studio 安装程序中列为“可用”，而不是“已安装”。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
* [Visual Studio 安装和升级问题疑难解答](troubleshooting-installation-issues.md)
