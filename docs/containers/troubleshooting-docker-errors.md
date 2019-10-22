---
title: 在 Windows 上排查 Docker 客户端错误 | Microsoft Docs
description: 在 Windows 上通过使用 Visual Studio 排查在使用 Visual Studio 创建 Web 应用并将其部署到 Docker 时遇到的问题。
ms.technology: vs-azure
author: ghogen
manager: jillfra
ms.custom: seodec18
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.devlang: dotnet
ms.topic: conceptual
ms.workload: multiple
ms.date: 10/13/2017
ms.author: ghogen
ms.openlocfilehash: ca43098740a1e8e940f27eae8d2c4d405c23230b
ms.sourcegitcommit: 16d8ffc624adb716753412a22d586eae68a29ba2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "71125955"
---
# <a name="troubleshoot-visual-studio-development-with-docker"></a>使用 Docker 排查 Visual Studio 开发方面的问题

使用 Visual Studio 容器工具时，可能会在生成或调试应用程序过程中遇到问题。 以下是一些常见的故障排除步骤。

## <a name="volume-sharing-is-not-enabled-enable-volume-sharing-in-the-docker-ce-for-windows-settings--linux-containers-only"></a>未启用卷共享。 启用“Docker CE for Windows”设置中的卷共享（仅 Linux 容器）

若要解决此问题，请执行以下操作：

1. 右键单击通知区域中的“Docker for Windows”  ，并选择“设置”  。
1. 选择“共享驱动器”  ，并共享系统驱动器和项目所在的驱动器。

> [!NOTE]
> 如果文件显示“已共享”，可能仍需要单击对话框底部的“重置凭据...”链接，以便重新启用卷共享。 若要在重置凭据后继续，可能必须重启 Visual Studio。

![共享驱动器](media/troubleshooting-docker-errors/shareddrives.png)

> [!TIP]
> 如果未配置共享驱动器，Visual Studio 2017 版本 15.6 之后的版本会发出提示  。

### <a name="container-type"></a>容器类型

向项目添加 Docker 支持后，请选择 Windows 或 Linux 容器。 Docker 主机必须运行类型相同的容器。 要更改正在运行的 Docker 实例中的容器类型，请右键单击系统托盘中的 Docker 图标，再选择“切换到 Windows 容器...”或“切换到 Linux 容器...”   。

## <a name="unable-to-start-debugging"></a>无法开始调试

其中一个原因可能与在用户配置文件的文件夹中有过时调试组件有关。 请执行以下命令来删除这些文件夹，以便在下次调试会话上下载最新调试组件。

- del %userprofile%\vsdbg
- del %userprofile%\onecoremsvsmon

## <a name="errors-specific-to-networking-when-debugging-your-application"></a>调试应用程序时特定于网络的错误

尝试执行可从[清理容器主机网络](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/master/windows-server-container-tools/CleanupContainerHostNetworking)下载的脚本，此操作会刷新主机上的网络相关组件。

## <a name="mounts-denied"></a>装载被拒绝

使用 Docker for macOS 时，可能会遇到引用文件夹 /usr/local/share/dotnet/sdk/NuGetFallbackFolder 错误。 将文件夹添加到 Docker 中的“文件共享”选项卡

## <a name="docker-users-group"></a>Docker 用户组

使用容器时，可能会在 Visual Studio 中遇到以下错误：

```
The current user must be in the 'docker-users' group to use Docker Desktop. 
Add yourself to the 'docker-users' group and then log out of Windows.
```

必须是“docker-users”组的成员，才有使用 Docker 容器的权限。  若要将自己添加到 Windows 10 中的组，请执行以下步骤：

1. 从“开始”菜单中，打开“计算机管理”  。
1. 展开“本地用户和组”，并选择“组”   。
1. 找到“docker-users”组，右键单击并选择“添加到组”   。
1. 添加用户帐户或帐户。
1. 注销后再次登录，以使更改生效。

还可以在管理员命令提示符下使用 `net localgroup` 命令向特定组添加用户。

```cmd
net localgroup docker-users DOMAIN\username /add
```

在 PowerShell 中，使用 [Add-LocalGroupMember](/powershell/module/microsoft.powershell.localaccounts/add-localgroupmember) 函数。

## <a name="microsoftdockertools-github-repo"></a>Microsoft/DockerTools GitHub 存储库

有关可能会遇到的其他任何问题，请参阅 [Microsoft/DockerTools](https://github.com/microsoft/dockertools/issues) 问题。