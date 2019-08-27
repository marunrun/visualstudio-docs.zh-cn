---
title: 部署到本地文件夹
description: 将应用部署到本地文件夹
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 3fa0569739ee81ec4b2aa0eec8157068ffc949cd
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149218"
---
1. 在中**解决方案资源管理器**，右键单击项目节点并选择**发布**(Web 窗体**发布 Web 应用**)。

    如果先前配置了任何发布配置文件，则“发布”窗格会显示  。 单击**新的配置文件**。

1. 在中**发布**对话框中，选择**文件夹**，单击**浏览**，并创建一个新文件夹**C:\Publish**。

    ![RemoteDBG_Publish_Local](../media/remotedbg_publish_local.png "RemoteDBG_Publish_Local")

    对于 Web 窗体应用中，选择**自定义**在发布对话框中，输入配置文件名称，然后选择**确定**。

1. 单击**创建配置文件**下拉列表中 (**发布**是默认值)。

1. 在中**发布**对话框中，单击**设置**链接，然后再选择**设置**选项卡。

1. 将配置设置为**调试**，选择**删除所有现有的文件发布前**，然后单击**保存**。

    > [!NOTE]
    > 如果使用发布版本，则禁用调试的 web.config 文件中，当你发布时。

1. 单击“发布”  。

    ![RemoteDBG_Publish_Debug_Config](../media/remotedbg_publish_debug_config.png "RemoteDBG_Publish_Debug_Config")

    应用程序将发布**调试**到本地文件夹的项目配置。 在输出窗口中显示进度。

1. 将 ASP.NET 项目目录从 Visual Studio 计算机复制到配置为 ASP.NET 应用程序的本地目录 (在此示例中， **C:\Publish**) Windows Server 计算机上。 在本教程中，我们假定您要手动复制，但可以使用 PowerShell、 Xcopy 或 Robocopy 等其他工具。

    > [!CAUTION]
    > 如果需要更改代码或重新生成，必须重新发布并重复此步骤。 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。    如果您不这样做将收到`cannot find or open the PDB file`警告在 Visual Studio 中，当您尝试调试进程时。

1. 在 Windows 服务器上，验证可以正确运行应用，通过在浏览器中打开应用。

    如果应用程序无法正常运行，在你的服务器和在 Visual Studio 计算机上安装 ASP.NET 的版本之间可能存在不匹配或可能使用 IIS 或网站配置存在问题。 重新检查前面的步骤。
