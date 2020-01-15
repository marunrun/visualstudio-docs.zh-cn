---
title: 在本地 Docker 容器中调试应用 | Microsoft Docs
description: 了解如何通过编辑和刷新以及设置调试断点功能来修改本地 Docker 容器中运行的应用以及刷新容器。
ms.author: ghogen
author: ghogen
manager: jillfra
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.topic: conceptual
ms.workload: multiple
ms.date: 07/25/2019
ms.technology: vs-azure
ms.openlocfilehash: 48754834295a552e3b189ff05ff2d1c12cd221a3
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75400907"
---
# <a name="debug-apps-in-a-local-docker-container"></a>在本地 Docker 容器中调试应用

Visual Studio 提供了一种一致方法来开发 Docker 容器，并在本地验证应用程序。 可以在安装了 Docker 的本地 Windows 桌面上运行的 Linux 或 Windows 容器中运行和调试应用，且每次更改代码时都无需重新启动容器。

本文介绍了如何使用 Visual Studio 在本地 Docker 容器中启动应用、进行更改，并刷新浏览器以查看所做的更改。 本文还介绍了如何为容器化的应用设置用于调试的断点。 支持的项目类型包括 .NET Framework 和 .NET Core Web 及控制台应用。 本文使用 ASP.NET Core Web 应用和 .NET Framework 控制台应用。

如果你具有支持类型的项目，则 Visual Studio 可以创建 Dockerfile 并将项目配置为在容器中运行。 请参阅 [Visual Studio 中的容器工具](overview.md)。

## <a name="prerequisites"></a>先决条件

若要在本地 Docker 容器中调试应用，必须安装以下工具：

::: moniker range="vs-2017"

* 安装了 Web 开发工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

* 安装了 Web 开发工作负荷的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

若要在本地运行 Docker 容器，必须安装本地 Docker 客户端。 你可以使用 [Docker 工具箱](https://www.docker.com/products/docker-toolbox)，这需要禁用 Hyper-V。 也可以使用[用于 Windows 的 Docker](https://www.docker.com/get-docker)，它使用 Hyper-V 并要求安装 Windows 10。

Docker 容器可用于 .NET Framework 和 .NET Core 项目。 请看以下两个示例。 首先，我们来了解一下 .NET Core Web 应用。 接下来，我们来了解 .NET Framework 控制台应用。

## <a name="create-a-web-app"></a>创建 Web 应用

如果你有一个项目，并且已按照[概述](overview.md)中的说明添加了 Docker 支持，请跳过此部分。

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range=">= vs-2019"
[!INCLUDE [create-aspnet5-app-2019](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end

### <a name="edit-your-code-and-refresh"></a>编辑代码并刷新

若要快速循环访问所做的更改，可以在容器中启动应用程序。 然后，继续进行更改，就像查看 IIS Express 一样查看这些更改。

1. 请确保 Docker 设置为使用你所使用的容器类型（Linux 或 Windows）。 右键单击任务栏上的 Docker 图标，然后选择相应的“切换到 Linux 容器”  或“切换到 Windows 容器”  。

1. 将“解决方案配置”设置为“调试”   。 然后，按 Ctrl+F5 以生成 Docker 映像并在本地运行该映像   。

    在 Docker 容器中生成映像并运行该映像后，Visual Studio 会在默认浏览器中启动 Web 应用。

1. 转到“索引”页  。 我们将在此页上进行更改。
1. 返回到 Visual Studio 并打开 Index.cshtml  。
1. 将以下 HTML 内容添加到文件末尾，然后保存所做的更改。

    ```html
    <h1>Hello from a Docker container!</h1>
    ```

1. 在输出窗口中，在 .NET 生成完成并看到下面的行后，切换回浏览器并刷新页面：

   ```output
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down.
   ```

你的更改已应用！

### <a name="debug-with-breakpoints"></a>使用断点进行调试

通常，需要对所做的更改进行进一步检查。 可以使用 Visual Studio 的调试功能来完成此任务。

1. 在 Visual Studio 中，打开 Index.cshtml.cs  。
2. 将 `OnGet` 方法的内容替换为以下代码：

   ```csharp
       ViewData["Message"] = "Your application description page from within a container";
   ```

3. 在代码行的左侧设置一个断点。
4. 要启动调试并命中断点，请按 F5。
5. 切换到 Visual Studio 以查看断点。 检查值。

   ![断点](media/edit-and-refresh/breakpoint.png)

## <a name="create-a-net-framework-console-app"></a>创建 .NET Framework 控制台应用

使用 .NET Framework 控制台应用项目时，不支持在没有业务流程的情况下添加 Docker 支持的方式。 即使仅使用单个 Docker 项目，你仍可以使用以下过程。

1. 创建新的 .NET Framework 控制台应用项目。
1. 在解决方案资源管理器中，右键单击项目节点，然后选择“添加” > “容器业务流程支持”   。  在出现的对话框中，选择“Docker Compose”  。 将 Dockerfile 添加到项目中，并添加一个包含相关支持文件的 Docker Compose 项目。

### <a name="debug-with-breakpoints"></a>使用断点进行调试

1. 在解决方案资源管理器中，打开 Program.cs  。
2. 将 `Main` 方法的内容替换为以下代码：

   ```csharp
       System.Console.WriteLine("Hello, world!");
   ```

3. 在代码行的左侧设置一个断点。
4. 要启动调试并命中断点，请按 F5。
5. 切换到 Visual Studio 以查看断点，并检查值。

   ![断点](media/edit-and-refresh/breakpoint-console.png)

## <a name="container-reuse"></a>容器重复使用

在开发周期中，Visual Studio 在你更改 Dockerfile 后仅重新生成容器映像和容器本身。 如果不更改 Dockerfile，Visual Studio 将重复使用以前运行的容器。

如果你手动修改了容器，并希望使用干净的容器映像重启，请使用 Visual Studio 中的“Build” > “Clean”命令，然后按常规操作生成   。

## <a name="troubleshoot"></a>疑难解答

了解如何对 [Visual Studio Docker 开发进行故障排除](troubleshooting-docker-errors.md)。

## <a name="next-steps"></a>后续步骤

有关更多详细信息，请参阅 [Visual Studio 如何构建容器化应用](container-build.md)。

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>有关 Visual Studio、Windows 和 Azure 中 Docker 的详细信息

* 详细了解[使用 Visual Studio 进行容器开发](/visualstudio/containers)。
* 要生成和部署 Docker 容器，请参阅 [Azure Pipelines 的 Docker 集成](https://aka.ms/dockertoolsforvsts)。
* 有关 Windows Server 和 Nano Server 文章的索引，请参阅 [Windows 容器信息](https://aka.ms/containers)。
* 详细了解 [Azure Kubernetes 服务](https://azure.microsoft.com/services/kubernetes-service/)并查看 [Azure Kubernetes 服务文档](/azure/aks)。
