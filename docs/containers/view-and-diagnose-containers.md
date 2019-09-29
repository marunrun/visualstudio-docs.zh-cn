---
title: 容器日志、环境变量与文件系统访问
description: 介绍如何通过使用工具窗口查看托管应用的容器内正在进行的操作，提高在 Visual Studio 中调试和诊断基于容器的应用的能力。
author: ghogen
ms.author: ghogen
ms.topic: conceptual
ms.date: 05/06/2019
ms.technology: vs-azure
monikerRange: vs-2019
ms.openlocfilehash: 3fb9a52f990a2e492c63a6e71a7cc2063110c816
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "71126093"
---
# <a name="how-to-view-and-diagnose-containers-in-visual-studio"></a>如何在 Visual Studio 中查看和诊断容器

可使用“容器”窗口查看托管应用的容器内发生的情况  。 如果习惯于通过使用命令提示符运行 Docker 命令来查看和诊断容器中进行的操作，则此窗口提供更方便的方法，在无需离开 Visual Studio IDE 的情况下即可监视容器。

> [!NOTE]
> “容器”窗口当前以预览扩展的形式提供，你可以[下载](https://aka.ms/vscontainerspreview)适用于 Visual Studio 2019 的预览扩展。

## <a name="prerequisites"></a>系统必备

- [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- 安装 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
- 安装[容器窗口扩展](https://aka.ms/vscontainerspreview)

## <a name="view-information-about-your-containers"></a>查看容器的相关信息

启动容器化 .NET 项目时，自动打开“容器”窗口  。 若要随时在 Visual Studio 中查看容器，请使用 Ctrl+Q 激活 Visual Studio 搜索框，键入 `Containers` 并选择第一项   。 还可以从主菜单中打开“容器”窗口  。 使用菜单路径“查看” > “其他 Windows” > “容器”    。  

![“容器”窗口中“环境”选项卡的屏幕截图](media/view-and-diagnose-containers/container-window.png)

在左侧，可看到本地计算机上的容器列表。 与解决方案关联的容器显示在“解决方案容器”下  。 在右侧，可看到一个窗格，其中包含“环境”、“端口”、“日志”和“文件”选项卡     。

> [!TIP]
> 可轻松自定义“容器”工具窗口在 Visual Studio 中的停靠位置  。 请参阅[在 Visual Studio 中自定义窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio)。 默认情况下，调试器正在运行时，“容器”窗口与“监视”窗口停靠在一起   。

## <a name="view-environment-variables"></a>查看环境变量

“环境”选项卡显示容器中的环境变量  。 对于应用的容器，可以通过多种方式设置这些变量，例如，在 Dockerfile 中，在 .env 文件中，或使用 Docker 命令启动容器时使用 -e 选项进行设置。

![“容器”窗口中“环境”选项卡的屏幕截图](media/view-and-diagnose-containers/container-environment-vars.png)

> [!NOTE]
> 对环境变量所做的任何更改都不会实时反映出来。 此外，此选项卡中的环境变量是容器上的系统环境变量，不反映应用程序的本地用户环境变量。

## <a name="view-port-mappings"></a>查看端口映射

在“端口”选项卡上，可以检查对容器有效的端口映射  。

![“容器”窗口中“端口”选项卡的屏幕截图](media/view-and-diagnose-containers/container-ports.png)

已链接已知端口，因此，如果某个端口上有可用的内容，则可以单击该链接打开浏览器。

## <a name="view-logs"></a>查看日志

“日志”选项卡显示 `docker logs` 命令的结果  。 该选项卡默认显示容器上的 stdout 和 stderr 流，但你可以配置输出。 有关详细信息，请参阅 [Docker 日志记录](https://docs.docker.com/config/containers/logging/)。  “日志”选项卡默认流式传输日志，但你可以通过选择选项卡上的“停止”按钮来禁用流式传输   。

![“容器”窗口中“日志”选项卡的屏幕截图](media/view-and-diagnose-containers/containers-logs.jpg)

若要清除日志，请使用“日志”选项卡上的“清除”按钮   。若要获取所有日志，请使用“刷新”按钮  。

> [!NOTE]
> Visual studio 会将 stdout 和 stderr 自动重定向到“输出”窗口，因此从 Visual Studio 启动的容器（即“解决方案容器”部分中的容器）不会显示此选项卡中的日志；请改为使用“输出”窗口    。

## <a name="view-the-filesystem"></a>查看 filesystem

在“文件”选项卡上，可以查看容器的文件系统，包括其中包含项目的应用文件夹  。

![“容器”窗口中“文件”选项卡的屏幕截图](media/view-and-diagnose-containers/container-filesystem.png)

若要在 Visual Studio 中打开文件，请浏览到该文件并双击它，或右键单击并选择“打开”  。 Visual Studio 在只读模式下打开文件。

![在 Visual Studio 中打开以供查看的文件的屏幕截图](media/view-and-diagnose-containers/container-file-open.png)

使用“文件”选项卡，可以查看容器的文件系统中的应用程序日志（例如 IIS 日志）、配置文件和其他内容文件  。

## <a name="start-stop-and-remove-containers"></a>启动、停止和删除容器

“容器”窗口默认显示 Docker 管理的计算机上的所有容器  。 可以使用工具栏按钮来启动、停止或移除（删除）不再需要的容器。  创建或删除容器时，会动态更新此列表。

## <a name="next-steps"></a>后续步骤

阅读[容器工具概述](overview.md)，了解有关 Visual Studio 中提供的容器工具的详细信息。

## <a name="see-also"></a>请参阅

[在 Visual Studio 进行容器开发](/visualstudio/containers)

[适用于 Visual Studio 的扩展市场](https://marketplace.visualstudio.com/)
