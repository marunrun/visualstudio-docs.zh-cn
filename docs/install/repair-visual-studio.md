---
title: 修复 Visual Studio
titleSuffix: ''
description: 了解如何修复 Visual Studio 2017 的安装
ms.date: 07/31/2019
ms.custom: seodec18
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 368ca6619a2fcff48cc3bcc7eb70913247b631b2
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114744"
---
# <a name="repair-visual-studio"></a>修复 Visual Studio

::: moniker range="vs-2017"

Visual Studio 安装有时会损毁或损坏。 通过修复可以解决此问题。

1. 在计算机上找到 Visual Studio 安装程序  。

     例如，在运行 Windows 10 周年更新或更高版本的计算机上，选择“开始”  ，再滚动到字母“V”  （其中它被列为“Visual Studio 安装程序”  ）。

   > [!NOTE]
   > 对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。
   >
   > 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 打开安装程序，选择“更多”  ，然后选择“修复”  。

    ![从 Visual Studio 安装程序修复 Visual Studio](media/repair-visual-studio.png "从 Visual Studio 安装程序修复 Visual Studio")

   > [!NOTE]
   > 修复 Visual Studio 将重置环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 将还原主题、颜色、键绑定等同步设置。
   >

   > [!TIP]
   > “修复”  选项仅对已安装的 Visual Studio 实例显示。 如果没有看到“修复”  选项，很可能是因为选择“更多”  时所在的版本在 Visual Studio 安装程序中列为“可用”，而不是“已安装”。

::: moniker-end

::: moniker range="vs-2019"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出    。

     ![打开 Visual Studio 安装程序](media/vs-2019/vs-installer-windows-start.png "打开 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本。 接下来，选择“更多”  ，然后选择“修复”  。

     ![修复 Visual Studio 2019](media/vs-2019/vs-installer-repair.png "修复 Visual Studio 2019")

   > [!NOTE]
   > 修复 Visual Studio 将重置环境。 将删除无需提升权限即可安装的每用户扩展、用户设置和配置文件等本地自定义项。 将还原主题、颜色、键绑定等同步设置。
   >

   > [!TIP]
   > “修复”  选项仅对已安装的 Visual Studio 实例显示。 如果没有看到“修复”  选项，很可能是因为选择“更多”  时所在的版本在 Visual Studio 安装程序中列为“可用”，而不是“已安装”。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
* [Visual Studio 安装和升级问题疑难解答](troubleshooting-installation-issues.md)
