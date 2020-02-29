---
title: Linux 上的远程调试 .NET Core |Microsoft Docs
ms.date: 02/26/2020
ms.topic: conceptual
helpviewer_keywords:
- remote debugging, linux
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 23bc0fa990a79b1855ec382f42248a0f847c3c9c
ms.sourcegitcommit: 3d64bfb9bf85395357effe054db9a9afaa0be5ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/29/2020
ms.locfileid: "78200865"
---
# <a name="remote-debug-net-core-on-linux-using-ssh"></a>使用 SSH 在 Linux 上远程调试 .NET Core

从 Visual Studio 2017 开始，可以通过 SSH 附加到 Linux 上运行的 .NET Core 进程。 本文介绍如何设置调试以及如何进行调试。

## <a name="prerequisites"></a>必备条件

在 Visual Studio 计算机上，需要安装**ASP.NET 和 web 开发**工作负荷或 **.net Core 跨平台开发**工作负荷。

在 Linux 服务器上，需要安装 SSH 服务器，并将其解压缩，并安装 wget。 例如，在 Ubuntu 上，可以通过运行以下内容来实现此目的：

``` cmd
sudo apt-get install openssh-server unzip curl
```

## <a name="build-and-deploy-the-application"></a>生成并部署应用程序

准备应用程序以进行调试：

- 请考虑在生成应用程序时使用调试配置。 调试零售编译的代码（发布配置）比调试编译的代码更难。 如果需要使用 Release 配置，请先禁用仅我的代码。 若要禁用此设置，请选择 "**工具**" > **选项**" > **调试**"，然后取消选中 "**启用仅我的代码**"。

- 请确保将项目配置为生成[可移植的 pdb](https://github.com/OmniSharp/omnisharp-vscode/wiki/Portable-PDBs) （这是默认设置），并确保 PBD 与 DLL 位于同一位置。 若要在 Visual Studio 中配置此项，请右键单击该项目，然后选择 "**属性**" > **生成** > **高级** > **调试信息**"。

在调试之前，可以使用多种方法来部署应用。 例如，你能够：

- 将源复制到目标计算机，并在 Linux 计算机上生成 ```dotnet build```。

- 在 Windows 上生成应用程序，并将生成项目传输到 Linux 计算机。 （生成项目由应用程序本身、它可能依赖的任何运行库以及 *.deps.json*文件组成。）

## <a name="attach-the-debugger"></a>附加调试器

配置计算机后，在 Linux 计算机上启动该应用程序，然后便可以附加该调试器。

1. 在 Visual Studio 中，选择 "**调试**" > "**附加到进程 ...** "。

1. 在 "**连接类型**" 列表中，选择 " **SSH**"。

1. 将**连接目标**更改为目标计算机的 IP 地址或主机名。

1. 查找要调试的进程。

   你的代码在唯一进程名称或名为 dotnet 的进程中运行。 若要查找你感兴趣的进程，请检查 " **Title** " 列，其中显示了该进程的命令行参数。

   在下面的示例中，将在 "**附加到进程**" 对话框中显示的 SSH 传输上看到远程 Linux 计算机上的进程列表。

   ![附加到 Linux 进程](media/remote-debug-linux-over-ssh-attach.png)

1. 选择 **“附加”** 。

1. 在出现的对话框中，选择要调试的代码类型。 选择 "**托管（.Net Core For Unix）** "。

1. 使用 Visual Studio 调试功能来调试应用程序。

   在下面的示例中，你将看到 Visual Studio 调试器在远程 Linux 计算机上运行的代码的断点处停止。

   ![命中断点](media/remote-debug-linux-over-ssh-hit-breakpoint.png)