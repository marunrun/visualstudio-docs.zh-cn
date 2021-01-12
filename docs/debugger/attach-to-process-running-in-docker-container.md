---
title: 附加到在 Docker 容器上运行的进程
description: 了解如何使用 Visual Studio 调试在 Docker 容器中运行的应用
ms.date: 11/11/2020
ms.topic: conceptual
helpviewer_keywords:
- debugging, linux Docker container
- debugging, Docker container
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: f6e2b851057d924353e6e1e9a211fcbb294353c8
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761259"
---
# <a name="attach-to-a-process-running-on-a-docker-container"></a>附加到在 Docker 容器上运行的进程 

可以使用 Visual Studio 调试在 Windows Docker 容器或 Linux .NET Core Docker 容器中运行的应用。

## <a name="attach-to-a-process-running-on-a-linux-docker-container"></a> 附加到正在 Linux Docker 容器上运行的进程

可以使用“附加到进程”对话框，将 Visual Studio 调试器附加到正在本地或远程计算机的 Linux .NET Core Docker 容器中运行的进程。

> [!IMPORTANT]
> 若要使用此功能，必须安装 .NET Core 跨平台开发工作负载，并对源代码具有本地访问权限。

**附加到 Linux Docker 容器中正在运行的进程：**

1. 在 Visual Studio 中，选择“调试 > 附加到进程”(CTRL+ALT+P)，打开“附加到进程”对话框 。

![Visual Studio 中“附加到进程”对话框的屏幕截图，其中显示“Docker (Linux 容器)”连接类型。](../debugger/media/attach-process-menu.png "Attach_To_Process_Menu")

2. 将“连接类型”设置为“Docker (Linux 容器)”。
3. 通过“选择 Docker 容器”对话框选择“查找...”，以设置“连接目标”。

    可以在本地或远程调试 Docker 容器进程。

    **在本地调试 Docker 容器进程：**
    1. 将“Docker CLI 主机”设置为“本地计算机”。
    1. 从列表中选择要附加到的正在运行的容器，然后点击“确定”。

    ![“选择 Docker 容器”菜单](../debugger/media/select-docker-container.png "Select_Docker_Container_Menu")

    **B.远程调试 Docker 容器进程：**

    > [!NOTE]
    > 可通过两个选项远程连接到 Docker 容器中正在运行的进程。 第一个选项是使用 SSH，它适用于未在本地计算机上安装 Docker 工具的情况。  如果在本地安装了 Docker 工具，并且具有配置为接受远程请求的 Docker 守护程序，请尝试第二个选项 - 使用 Docker 守护程序。

    1. 若要通过 SSH 连接到远程计算机，请执行以下操作：*_
        1. 选择“添加...”_*，以连接到远程系统。<br/>
        ![连接到远程系统](../debugger/media/connect-remote-system.png "连接到远程系统")
        1. 成功连接到 SSH 或守护程序后，选择要附加到的正在运行的容器，然后点击“确定”。

    1. 若要通过 [Docker 守护程序](https://docs.docker.com/engine/reference/commandline/dockerd/)将目标设置为正在运行进程的远程容器，请执行以下操作：*_
        1. 在“Docker 主机(可选)”_*下，指定守护程序地址（即通过 TCP、IP 等），然后单击刷新链接。
        1. 成功连接到守护程序后，选择要附加到的正在运行的容器，然后点击“确定”。

4. 从“可用进程”列表中选择相应的容器进程并选择“附加”，开始在 Visual Studio 中调试 C# 容器进程！

    ![Visual Studio 中“附加到进程”对话框的屏幕截图。连接类型设置为“Docker (Linux 容器)”，并且已选中 dotnet 进程。](../debugger/media/docker-attach-complete.png "已完成的 Linux Docker 附加菜单")

## <a name="attach-to-a-process-running-on-a-windows-docker-container"></a> 附加到正在 Windows Docker 容器上运行的进程

可以使用“附加到进程”对话框将 Visual Studio 调试器附加到正在本地计算机的 Windows Docker 容器中运行的进程。

> [!IMPORTANT]
> 若要对 .NET Core 进程使用此功能，必须安装 .NET Core 跨平台开发工作负载，并对源代码具有本地访问权限。

**附加到 Windows Docker 容器中正在运行的进程：**

1. 在 Visual Studio 中，选择“调试 > 附加到进程”（或 CTRL+ALT+P），打开“附加到进程”对话框  。

   ![Visual Studio 中“附加到进程”对话框的屏幕截图，其中显示“Docker (Windows 容器)”连接类型。](../debugger/media/attach-process-menu-docker-windows.png "Attach_To_Process_Menu")

2. 将“连接类型”设置为“Docker (Windows 容器)”。
3. 使用“选择 Docker 容器”对话框选择“查找...”，以设置“连接目标”。

    > [!IMPORTANT]
    > 目标进程必须与运行它的 Docker Windows 容器具有相同的处理器体系结构。

   当前无法通过 SSH 将目标设置为远程容器，而只能使用 Docker 守护程序来完成。

    若要通过 [Docker 守护程序](https://docs.docker.com/engine/reference/commandline/dockerd/)将目标设置为正在运行进程的远程容器，请执行以下操作：*_
    1. 在“Docker 主机(可选)”_*下，指定守护程序地址（即通过 TCP、IP 等），然后单击刷新链接。

    1. 成功连接到守护程序后，选择要附加到的正在运行的容器，然后选择“确定”。

4. 从“可用进程”列表中选择相应的容器进程并选择“附加”，以开始调试 C# 容器进程。

    ![Visual Studio 中“附加到进程”对话框的屏幕截图。连接类型设置为“Docker (Windows 容器)”，并且已选中 dotnet.exe 进程。](../debugger/media/docker-attach-complete-windows.png "已完成的 Windows Docker 附加菜单")

5. 从可用进程列表中选择相应的容器进程并选择“附加”，以开始调试 C# 容器进程。