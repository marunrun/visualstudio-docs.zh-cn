---
title: 在 Windows 上排查 Docker 客户端错误 | Microsoft Docs
description: 在 Windows 上通过使用 Visual Studio 排查在使用 Visual Studio 创建 Web 应用并将其部署到 Docker 时遇到的问题。
ms.technology: vs-azure
author: ghogen
manager: jillfra
ms.custom: seodec18
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.devlang: dotnet
ms.topic: troubleshooting
ms.workload: multiple
ms.date: 01/27/2020
ms.author: ghogen
ms.openlocfilehash: 9535a7d88cb375d97867092eddf969095c327329
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2020
ms.locfileid: "97729234"
---
# <a name="troubleshoot-visual-studio-development-with-docker"></a>使用 Docker 排查 Visual Studio 开发方面的问题

使用 Visual Studio 容器工具时，可能会在生成或调试应用程序过程中遇到问题。 以下是一些常见的故障排除步骤。

## <a name="volume-sharing-is-not-enabled-enable-volume-sharing-in-the-docker-ce-for-windows-settings--linux-containers-only"></a>未启用卷共享。 启用“Docker CE for Windows”设置中的卷共享（仅 Linux 容器）

只有在将 Hyper-V 与 Docker 一起使用时，才需要管理文件共享。 如果使用的是 WSL 2，则无需执行以下步骤，并且文件共享选项将不可见。 若要解决此问题，请执行以下操作：

1. 右键单击通知区域中的“Docker for Windows”  ，并选择“设置”  。
1. 选择“资源” > “文件共享”并共享需要访问的文件夹 。 可以共享整个系统驱动器，但不建议这样做。

    ![共享驱动器](media/troubleshooting-docker-errors/docker-settings-image.png)

> [!TIP]
> 如果未配置共享驱动器，Visual Studio 2017 版本 15.6 之后的版本将发出提示。

## <a name="unable-to-start-debugging"></a>无法开始调试

其中一个原因可能与在用户配置文件的文件夹中有过时调试组件有关。 请执行以下命令来删除这些文件夹，以便在下次调试会话上下载最新调试组件。

- del %userprofile%\vsdbg
- del %userprofile%\onecoremsvsmon

## <a name="errors-specific-to-networking-when-debugging-your-application"></a>调试应用程序时特定于网络的错误

尝试执行可从[清理容器主机网络](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/master/windows-server-container-tools/CleanupContainerHostNetworking)下载的脚本，此操作会刷新主机上的网络相关组件。

## <a name="mounts-denied"></a>装载被拒绝

使用 Docker for macOS 时，可能会遇到引用文件夹 /usr/local/share/dotnet/sdk/NuGetFallbackFolder 错误。 将文件夹添加到 Docker 中的“文件共享”选项卡。

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

## <a name="low-disk-space"></a>磁盘空间不足

默认情况下，Docker 将映像存储在 %ProgramData%/Docker/ 文件夹中，该文件夹通常位于系统驱动器 *C:\ProgramData\Docker\*。 若要防止映像占用系统驱动器上的宝贵空间，可以更改映像文件夹位置。 为此，请执行以下操作：

 1. 右键单击任务栏上的 Docker 图标并选择“设置”。
 1. 选择“Docker 引擎”。 
 1. 在编辑窗格中，添加带有 Docker 映像所需位置值的 `graph` 属性设置：

```json
    "graph": "D:\\mypath\\images"
```

![Docker 文件共享的屏幕截图](media/troubleshooting-docker-errors/docker-daemon-settings.png)

单击“应用和重启”。 这些步骤会修改 %ProgramData%\docker\config\daemon.json 的配置文件  。 以前生成的映像不会移动。

## <a name="container-type-mismatch"></a>容器类型不匹配

向项目添加 Docker 支持后，请选择 Windows 或 Linux 容器。 如果 Docker 服务器主机未配置为运行与项目目标相同的容器类型，则你可能会看到类似以下错误：

![Docker 主机和项目不匹配的屏幕截图](media/troubleshooting-docker-errors/docker-host-config-change-linux-to-windows.png)

要解决此问题：

- 右键单击系统栏中的“用于 Windows 的 Docker”图标，然后选择“切换到 Windows 容器…”或“切换到 Linux 容器…” 。

## <a name="microsoftdockertools-github-repo"></a>Microsoft/DockerTools GitHub 存储库

有关可能会遇到的其他任何问题，请参阅 [Microsoft/DockerTools](https://github.com/microsoft/dockertools/issues) 问题。

## <a name="see-also"></a>请参阅

- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
