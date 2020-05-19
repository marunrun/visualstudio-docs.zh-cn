---
title: 远程调试 Linux 上的 .NET Core | Microsoft Docs
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/29/2020
ms.locfileid: "78200865"
---
# <a name="remote-debug-net-core-on-linux-using-ssh"></a>使用 SSH 远程调试 Linux 上的 .NET Core

从 Visual Studio 2017 开始，可通过 SSH 附加到在 Linux 上运行的 .NET Core 进程。 本文介绍调试的设置方法和调试方法。

## <a name="prerequisites"></a>先决条件

在 Visual Studio 计算机上，需要安装“ASP.NET 和 Web 开发”工作负载或“.NET Core 跨平台开发”工作负载 。

在 Linux 服务器上，需要安装 SSH 服务器，可使用 curl 或 wget 解压缩并安装。 例如，在 Ubuntu 上，可以通过运行以下内容来实现此目的：

``` cmd
sudo apt-get install openssh-server unzip curl
```

## <a name="build-and-deploy-the-application"></a>生成并部署应用程序

准备应用程序以进行调试：

- 生成应用程序时，请考虑使用“调试”配置。 调试零售编译代码（发布配置）比调试编译代码要困难得多。 如果需要使用“发布”配置，请先禁用“仅我的代码”。 若要禁用此设置，请选择“工具” > “选项” > “调试”，然后选择“启用仅我的代码”   。

- 请确保项目配置为生成[可移植 PDB](https://github.com/OmniSharp/omnisharp-vscode/wiki/Portable-PDBs)（默认设置），并确保 PDB 与 DLL 处于同一位置。 若要在 Visual Studio 中配置此项目，请右键单击它，然后选择“属性” > “生成” > “高级” > “调试信息”   。

在调试之前，可以使用多种方法来部署应用。 例如，你可以：

- 将源复制到目标计算机，并在 Linux 计算机上使用 ```dotnet build``` 进行生成。

- 在 Windows 上生成应用，并将生成项目传输到 Linux 计算机。 （生成工件包含应用程序本身、它可能依赖的任何运行时库和 .deps.json 文件。）

## <a name="attach-the-debugger"></a>附加调试器

配置计算机后，在 Linux 计算机上启动应用程序，然后准备好附加调试器。

1. 在 Visual Studio 中，选择“调试” > “附加到进程…” 。

1. 在“连接类型”列表中，选择“SSH” 。

1. 将“连接目标”更改为目标计算机的 IP 地址或主机名。

1. 查找要调试的进程。

   代码以唯一的进程名或名为 dotnet 的进程运行。 若要查找你感兴趣的进程，请查看“Title”列，该列显示了进程的命令行参数。

   在下面的示例中，你将在“附加到进程”对话框中显示的 SSH 传输上看到远程 Linux 计算机中的进程列表。

   ![附加到 Linux 进程](media/remote-debug-linux-over-ssh-attach.png)

1. 选择 **“附加”** 。

1. 在显示的对话框中，选择要调试的代码类型。 选择“托管(.NET Core for Unix)”。

1. 使用 Visual Studio 调试功能来调试应用。

   在下面的示例中，你将看到 Visual Studio 调试器在远程 Linux 计算机上运行的代码断点停止。

   ![命中断点](media/remote-debug-linux-over-ssh-hit-breakpoint.png)