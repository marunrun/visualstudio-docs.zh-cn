---
title: 修改 Visual Studio
titleSuffix: ''
description: 了解如何逐步修改 Visual Studio。
ms.custom: H1Hack27Feb2017,seodec18
ms.date: 07/31/2019
ms.topic: conceptual
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ad5b8a0c261ed967710480b0abd3a2b9d34f01ce
ms.sourcegitcommit: 5694c5236fa32ba7f5bc1236a853f725ec7557e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2019
ms.locfileid: "68681397"
---
# <a name="modify-visual-studio-by-adding-or-removing-workloads-and-components"></a>通过添加或删除工作负载和组件修改 Visual Studio

::: moniker range="vs-2019"

可轻松修改 Visual Studio，使其在你需要时包含想要的内容。 为此，请打开 Visual Studio 安装程序以添加或删除工作负载和组件。

::: moniker-end

::: moniker range="vs-2017"

我们不但简化了 Visual Studio 的个性化设置，让用户能够轻松匹配所需完成的任务，还简化了 Visual Studio 的自定义操作。 要执行此操作，请启动新的 Visual Studio 安装程序，即可进行所需更改。

::: moniker-end

操作方法如下。

## <a name="modify-workloads"></a>修改工作负载

 工作负载包含所用编程语言或平台必需的功能。 可以使用工作负载来修改 Visual Studio，以便在需要执行某项操作时为其提供支持。

>[!IMPORTANT]
>若要安装、更新或修改 Visual Studio，必须使用具有管理权限的帐户登录。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。

>[!TIP]
> 以下过程假定你具有 Internet 连接。 有关如何修改先前创建的 Visual Studio [脱机安装](create-an-offline-installation-of-visual-studio.md)的详细信息，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)页。

::: moniker range="vs-2017"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出    。

     ![Visual Studio 安装程序](media/vs2017-locate-the-visual-studio-installer.PNG "查找 Microsoft Visual Studio 安装程序")

     >[!NOTE]
     >对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。<br/><br/> 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 单击或点击以启动安装程序，然后选择“修改”  。

     ![启动或修改 Visual Studio](media/modify-visual-studio.png "修改 Visual Studio 2017")

     如果还有更新挂起，则“修改”按钮会出现在其他位置。 这样一来，如果选择执行此操作，可以在不更新的情况下修改 Visual Studio。 单击“更多”，然后选择“修改”   。

     ![更新或修改 Visual Studio](media/modify-or-update-visual-studio.png "更新或修改 Visual Studio 2017")

1. 从“工作负载”  屏幕中，选择或取消选择要安装或卸载的工作负载。

    ![Visual Studio 2017 设置对话框](media/vs2017-modify-workloads.PNG "选择 Visual Studio 2017 中的工作负载")

1. 再一次选择“修改”  。

1. 安装完新的工作负载和组件后，选择“启动”  。

::: moniker-end

::: moniker range="vs-2019"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出    。

     ![从 Windows 打开 Visual Studio 安装程序](media/vs-2019/vs-installer-windows-start.png "打开 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本，然后选择“修改”  。

     ![更新或修改 Visual Studio](media/vs-2019/vs-installer-modify.png "更新或修改 Visual Studio 2019")

1. 在“工作负载”选项卡中，选择或取消选择要安装或卸载的工作负载  。

    ![Visual Studio 2019 设置对话框](media/vs-2019/vs-installer-modify-workloads.png "选择 Visual Studio 2019 中的工作负载")

1. 选择是要接受默认的“下载时安装”选项还是“全部下载后再安装”选项   。

    ![Visual Studio 2019 安装选项](media/vs-2019/vs-installer-choose-install-or-download.png "选择下载时安装或先下载稍后再安装")

    如果想要先下载稍后再安装，则“全部下载后再安装”选项很有用。

1. 选择“修改”  。

1. 安装完新的工作负载和组件后，从 Visual Studio 安装程序中选择“启动”  。

::: moniker-end

## <a name="modify-individual-components"></a>修改各个组件

如果不想通过安装工作负载来自定义 Visual Studio 安装，请从 Visual Studio 安装程序中选择“各个组件”选项卡，选择所需组件，然后按提示操作  。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [更新 Visual Studio](update-visual-studio.md)
* [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
* [在维修基线上更新 Visual Studio](update-servicing-baseline.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
