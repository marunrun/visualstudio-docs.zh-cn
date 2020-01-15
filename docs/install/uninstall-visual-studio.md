---
title: 卸载 Visual Studio
titleSuffix: ''
description: 了解如何逐步卸载 Visual Studio。
ms.date: 12/19/2019
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- uninstall
- uninstall Visual Studio
ms.assetid: 0e445255-b796-426d-ad93-a4d8e36da2c5
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: a895d9a94ada22ecce340488c6ba00662a599969
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594469"
---
# <a name="uninstall-visual-studio"></a>卸载 Visual Studio

此页面介绍如何卸载 Visual Studio（一个面向开发人员的工作效率工具集成套件）。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请查阅[卸载 Visual Studio for Mac](/visualstudio/mac/uninstall)。

::: moniker range="vs-2017"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 周年更新或更高版本的计算机上，选择“开始”  ，再滚动到字母“V”  （其中它被列为“Visual Studio 安装程序”  ）。

     ![Visual Studio 安装程序](media/locate-the-visual-studio-installer.png "找到 Microsoft Visual Studio 安装程序")

   > [!NOTE]
   > 对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。<br/><br/> 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 在安装程序中，查找已安装的 Visual Studio 版本。 接下来，选择“更多”  ，然后选择“卸载”  。

     ![卸载 Visual Studio 2017](media/uninstall-visual-studio.png "卸载 Visual Studio 2017")

1. 单击  “确定”确认所做选择。

如果以后改变主意，想重新安装 Visual Studio 2017，请再次启动 Visual Studio 安装程序，然后从选择屏幕中选择“安装”  。

## <a name="uninstall-visual-studio-installer"></a>卸载 Visual Studio 安装程序

若要从计算机中彻底删除 Visual Studio 2017 的所有安装内容和 Visual Studio 安装程序，请使用“应用和功能”进行卸载。

1. 在 Windows 10 的“在此键入进行搜索”框中，键入“应用和功能”  。
1. 查找“Microsoft Visual Studio 2017”（或“Visual Studio 2017”）   。
1. 选择“卸载”  。
1. 然后，查找“Microsoft Visual Studio 安装程序”  。
1. 选择“卸载”  。

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

1. 在安装程序中，查找已安装的 Visual Studio 版本。 接下来，选择“更多”  ，然后选择“卸载”  。

     ![卸载 Visual Studio 2019](media/vs-2019/vs-installer-uninstall.png "卸载 Visual Studio 2019")

1. 单击  “确定”确认所做选择。

     ![卸载 Visual Studio 确认](media/vs-2019/uninstall-visualstudio-confirm.png "确认是否要卸载 Visual Studio 2019")

如果稍后改变主意并想要重新安装 Visual Studio 2019，请再次启动 Visual Studio 安装程序，选择“可用”选项卡，选择要安装的 Visual Studio 版本，然后选择“安装”   。

## <a name="uninstall-visual-studio-installer"></a>卸载 Visual Studio 安装程序

若要从计算机中删除 Visual Studio 2019 的所有安装内容和 Visual Studio 安装程序，请使用“应用和功能”进行卸载。

1. 在 Windows 10 的“在此键入进行搜索”框中，键入“应用和功能”  。
1. 查找“Visual Studio 2019”  。
1. 选择“卸载”  。
1. 然后，查找“Microsoft Visual Studio 安装程序”  。
1. 选择“卸载”  。

::: moniker-end

## <a name="remove-all-files"></a>删除所有文件

如果遇到灾难性错误，并且无法使用上述说明卸载 Visual Studio，则可以考虑使用“最后一种方法”选项。 有关如何完全删除所有 Visual Studio 安装文件和产品信息的详细信息，请参阅[删除 Visual Studio](remove-visual-studio.md)页。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [修改 Visual Studio](modify-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)