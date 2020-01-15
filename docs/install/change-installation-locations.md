---
title: 选择安装位置
description: 了解如何通过将下载缓存、共享组件、SDK 和工具的位置更改到不同的驱动器来减少 Visual Studio 在系统驱动器上的安装占用。 例如，将 C 驱动器中的一些文件移动到 D 驱动器。
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- change installation locations for Visual Studio
- select an installation location for Visual Studio files
- move installation files to different drives
- use the D drive
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 3ea0651ee1cfde14d5ef7b422095707d8f81cb2f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590145"
---
# <a name="select-the-installation-locations-in-visual-studio"></a>在 Visual Studio 中选择安装位置

::: moniker range="vs-2019"

通过更改 Visual Studio 某些文件的位置，可以减少其在系统驱动器上的安装占用。 具体来说，下载缓存、共享组件、SDK 和工具文件可使用不同位置。

::: moniker-end

::: moniker range="vs-2017"

**15.7 版的新增功能：** 通过更改 Visual Studio 某些文件的位置，可以减少其在系统驱动器上的安装占用。 具体来说，下载缓存、共享组件、SDK 和工具文件可使用不同位置。

::: moniker-end

   > [!NOTE]
   > 某些工具和 SDK 对于安装位置有不同规则。 即使选择另一位置，这些工具和 SDK 也会安装在系统驱动器上。

准备好开始了吗？ 操作方法如下。

::: moniker range="vs-2017"

1. 安装 Visual Studio 时，选择“安装位置”选项卡  。

   ![Visual Studio 2017 - 选择安装位置](media/vs-installation-locations.png "选择安装位置。")

1. 在“Visual Studio IDE”部分中，接受默认值  。 Visual Studio 将安装核心产品并包含特定于此版本的 Visual Studio 的文件。

   ![“安装位置”选项卡的“Visual Studio IDE”部分](media/vs-installation-locations-ide.png "接受“安装位置”选项卡的“Visual Studio IDE”部分的默认值。")

   > [!TIP]
   > 如果系统驱动器是固态硬盘 (SSD)，建议你接受系统驱动器上的默认位置。 原因？ 当使用 Visual Studio 进行开发时，将从大量文件进行读取并写入大量文件，这会增加磁盘 I/O 活动。 最好选择最快的驱动器来处理负载。

1. 在“下载缓存”部分，决定是否保留下载缓存，然后决定其文件的存储位置  。

     ![“安装位置”选项卡的“下载缓存”部分](media/vs-installation-locations-cache.png "选择安装完成后是否保留下载缓存，然后指定要存储文件的驱动器。")

    1. 选中或取消选中“安装完成后保留下载缓存”  。

       如果决定不保留下载缓存，则仅临时使用该位置。 此操作不会影响或删除以前的安装内容。

    1. 指定在其中存储下载缓存中的安装文件和清单的驱动器。

        例如，如果选择“使用 C++ 的桌面开发”工作负载，系统驱动器上临时需要的大小为 1.58 GB，安装完成后即会释放。

       > [!IMPORTANT]
       > 该位置在首次安装时进行设置，并且之后无法从安装程序 UI 中更改。 相反，必须[使用命令行参数](use-command-line-parameters-to-install-visual-studio.md)删除下载缓存。

1. 在“共享组件、工具和 SDK”部分，指定要存储由 Visual Studio 并行安装所共享的文件的驱动器  。 SDK 和工具也存储在此目录中。

   ![“安装位置”选项卡的“共享组件、工具和 SDK”部分](media/vs-installation-locations-shared.png "指定要存储共享组件、工具和 SDK 的位置。")

::: moniker-end

::: moniker range="vs-2019"

1. 安装 Visual Studio 时，选择“安装位置”选项卡  。

   ![Visual Studio 2019 - 选择安装位置](media/vs-2019/vs-installer-installation-locations.png "选择安装位置。")

1. 在“Visual Studio IDE”部分中，接受默认值  。 Visual Studio 将安装核心产品并包含特定于此版本的 Visual Studio 的文件。

   > [!TIP]
   > 如果系统驱动器是固态硬盘 (SSD)，建议你接受系统驱动器上的默认位置。 原因？ 当使用 Visual Studio 进行开发时，将从大量文件进行读取并写入大量文件，这会增加磁盘 I/O 活动。 最好选择最快的驱动器来处理负载。

1. 在“下载缓存”部分，决定是否保留下载缓存，然后决定其文件的存储位置  。

    * 选中或取消选中“安装完成后保留下载缓存”  。

       如果决定不保留下载缓存，则仅临时使用该位置。 此操作不会影响或删除以前的安装内容。

    * 指定在其中存储下载缓存中的安装文件和清单的驱动器。

        例如，如果选择“使用 C++ 的桌面开发”工作负载，系统驱动器上临时需要的大小为 1.58 GB，安装完成后即会释放。

       > [!IMPORTANT]
       > 该位置在首次安装时进行设置，并且之后无法从安装程序 UI 中更改。 相反，必须[使用命令行参数](use-command-line-parameters-to-install-visual-studio.md)删除下载缓存。

1. 在“共享组件、工具和 SDK”部分中，请注意它使用在“下载缓存”部分中选择的同一驱动器  。 Visual Studio 在\Microsoft\VisualStudio\Shared 目录中存储由并行 Visual Studio 安装共享的文件。 SDK 和工具也存储在此目录中。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [修改 Visual Studio](update-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
