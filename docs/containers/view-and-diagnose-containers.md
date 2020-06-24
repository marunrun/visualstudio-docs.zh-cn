---
title: Docker 容器日志、环境变量与文件系统访问
description: 介绍如何通过使用工具窗口查看托管应用的容器内正在进行的操作，提高在 Visual Studio 中调试和诊断基于容器的应用的能力。
author: ghogen
ms.author: ghogen
ms.topic: how-to
ms.date: 01/20/2020
ms.technology: vs-azure
monikerRange: vs-2019
ms.openlocfilehash: c870378cf277a6008f17ec42d960e07e18a53e86
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283120"
---
# <a name="how-to-view-and-diagnose-containers-and-images-in-visual-studio"></a>如何在 Visual Studio 中查看和诊断容器与图像

可使用“容器”窗口查看托管应用的容器内发生的情况  。 如果习惯于通过使用命令提示符运行 Docker 命令来查看和诊断容器中进行的操作，则此窗口提供更方便的方法，在无需离开 Visual Studio IDE 的情况下即可监视容器。

## <a name="prerequisites"></a>先决条件

- [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- [Visual Studio 2019 版本 16.4 预览版 2](https://visualstudio.microsoft.com/downloads) 或更高版本，或者如果使用的是早期版本的 Visual Studio 2019，请安装[容器窗口扩展](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-containers-tools-extensions)。

## <a name="view-information-about-your-containers"></a>查看容器的相关信息

启动容器化 .NET 项目时，自动打开“容器”窗口  。 若要随时在 Visual Studio 中查看容器，请使用 Ctrl+Q 激活 Visual Studio 搜索框，键入 `Containers` 并选择第一项   。 还可以从主菜单中打开“容器”窗口  。 使用菜单路径“查看” > “其他 Windows” > “容器”    。  

![“容器”窗口中“环境”选项卡的屏幕截图](media/view-and-diagnose-containers/container-window.png)

在左侧，可看到本地计算机上的容器列表。 与解决方案关联的容器显示在“解决方案容器”下  。 在右侧，可看到一个窗格，其中包含“环境”、“端口”、“日志”和“文件”选项卡     。

> [!TIP]
> 可轻松自定义“容器”工具窗口在 Visual Studio 中的停靠位置  。 请参阅[在 Visual Studio 中自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)。 默认情况下，调试器正在运行时，“容器”窗口与“监视”窗口停靠在一起   。

## <a name="view-environment-variables"></a>查看环境变量

“环境”选项卡显示容器中的环境变量  。 对于应用的容器，可以通过多种方式设置这些变量，例如，在 Dockerfile 中，在 .env 文件中，或使用 Docker 命令启动容器时使用 -e 选项进行设置。

![“容器”窗口中“环境”选项卡的屏幕截图](media/view-and-diagnose-containers/containers-environment-vars.png)

> [!NOTE]
> 对环境变量所做的任何更改都不会实时反映出来。 此外，此选项卡中的环境变量是容器上的系统环境变量，不反映应用程序的本地用户环境变量。

## <a name="view-port-mappings"></a>查看端口映射

在“端口”选项卡上，可以检查对容器有效的端口映射  。

![“容器”窗口中“端口”选项卡的屏幕截图](media/view-and-diagnose-containers/containers-ports.png)

已链接已知端口，因此，如果某个端口上有可用的内容，则可以单击该链接打开浏览器。

## <a name="view-logs"></a>查看日志

“日志”选项卡显示 `docker logs` 命令的结果  。 该选项卡默认显示容器上的 stdout 和 stderr 流，但你可以配置输出。 有关详细信息，请参阅 [Docker 日志记录](https://docs.docker.com/config/containers/logging/)。  “日志”选项卡默认流式传输日志，但你可以通过选择选项卡上的“停止”按钮来禁用流式传输   。

![“容器”窗口中“日志”选项卡的屏幕截图](media/view-and-diagnose-containers/containers-logs.png)

若要清除日志，请使用“日志”选项卡上的“清除”按钮   。若要获取所有日志，请使用“刷新”按钮  。

> [!NOTE]
> 当你直接运行而不使用 Windows 容器进行调试时，Visual studio 会将 stdout 和 stderr 自动重定向到“输出”窗口，因此使用 Ctrl+F5 从 Visual Studio 启动的 Windows 容器不会显示此选项卡中的日志；请改为使用“输出”窗口     。

## <a name="view-the-filesystem"></a>查看 filesystem

在“文件”选项卡上，可以查看容器的文件系统，包括其中包含项目的应用文件夹  。

![“容器”窗口中“文件”选项卡的屏幕截图](media/view-and-diagnose-containers/container-filesystem.png)

若要在 Visual Studio 中打开文件，请浏览到该文件并双击它，或右键单击并选择“打开”  。 Visual Studio 在只读模式下打开文件。

![在 Visual Studio 中打开以供查看的文件的屏幕截图](media/view-and-diagnose-containers/container-file-open.png)

使用“文件”选项卡，可以查看容器的文件系统中的应用程序日志（例如 IIS 日志）、配置文件和其他内容文件  。

## <a name="start-stop-and-remove-containers"></a>启动、停止和删除容器

“容器”窗口默认显示 Docker 管理的计算机上的所有容器  。 可以使用工具栏按钮来启动、停止或移除（删除）不再需要的容器。  创建或删除容器时，会动态更新此列表。

## <a name="open-a-terminal-window-in-a-running-container"></a>在正在运行的容器中打开终端窗口

可以使用“容器”窗口中的“打开终端窗口”按钮在容器中打开终端窗口（命令提示符或交互式 shell）   。

![在“容器”窗口中打开终端窗口的屏幕截图](media/view-and-diagnose-containers/containers-open-terminal-window.png)

对于 Windows 容器，将打开 Windows 命令提示符。 对于 Linux 容器，将使用 bash shell 打开窗口。

![bash 窗口的屏幕截图](media/view-and-diagnose-containers/container-bash-window.png)

通常，终端窗口会在 Visual Studio 之外作为单独的窗口打开。 如果希望将命令行环境作为可停靠的工具窗口集成到 Visual Studio IDE 中，则可以安装 [Whack Whack Terminal](https://marketplace.visualstudio.com/items?itemName=DanielGriffen.WhackWhackTerminal)。

## <a name="attach-the-debugger-to-a-process"></a>将调试器附加到进程

可以使用“容器”窗口工具栏上的“附加到进程”  按钮，将调试器附加到正在容器中运行的进程。 使用此按钮时，将出现“附加到进程”  对话框，并显示正在容器中运行的可用进程。  

![“附加到进程”对话框的屏幕截图](media/view-and-diagnose-containers/containers-attach-to-process.jpg)

可以附加到容器中的托管进程。 若要查找另一个容器中的进程，请使用“查找”按钮，然后在“选择 Docker 容器”对话框中选择另一个容器   。

## <a name="viewing-images"></a>查看图像

还可以使用“容器”窗口中的“图像”选项卡来查看本地计算机上的图像   。 从外部存储库中提取的图像将在树视图中组合在一起。 选择一个图像以查看该图像的详细信息。

若要删除某个图像，请在树视图中右键单击该图像，然后选择“删除”  ，或选择该图像，然后使用工具栏上的“删除”  按钮。

## <a name="next-steps"></a>后续步骤

阅读[容器工具概述](overview.md)，了解有关 Visual Studio 中提供的容器工具的详细信息。

## <a name="see-also"></a>请参阅

[在 Visual Studio 进行容器开发](/visualstudio/containers)

[适用于 Visual Studio 的扩展市场](https://marketplace.visualstudio.com/)
