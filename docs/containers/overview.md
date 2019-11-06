---
title: Windows 上的 Visual Studio 容器工具
description: 了解 Visual Studio 中可用于 Docker 的工具
author: ghogen
ms.author: ghogen
ms.topic: overview
ms.date: 03/20/2019
ms.technology: vs-azure
ms.openlocfilehash: b60e5df4d94c290ca8aa7bf56471b5fed6c1879a
ms.sourcegitcommit: 97623fd6190c43fed0d2ee7af92b01c375282622
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73568897"
---
# <a name="container-tools-in-visual-studio"></a>Visual Studio 中的容器工具

Visual Studio 中用于使用容器进行开发的工具易于使用，并大大简化生成、调试和部署容器化应用程序的过程。 可以将容器用于单个项目，也可以将容器业务流程与 Docker Compose、Service Fabric 或 Kubernetes 结合使用，以便使用容器中的多个服务。

::: moniker range="vs-2017"

## <a name="prerequisites"></a>系统必备

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)   
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="docker-support-in-visual-studio"></a>Visual Studio 中的 Docker 支持

Docker 支持适用于 ASP.NET 项目、ASP.NET Core 项目，以及 .NET Core 和 .NET Framework 控制台项目。

Visual Studio 中的 Docker 支持因版本而异，以响应客户需求。 可以向项目添加两个级别的 Docker 支持，并且受支持的选项因项目类型和 Visual Studio 版本而异。 借助某些受支持的项目类型，如果只想将容器用于单个项目，而不使用业务流程，则可以通过添加 Docker 支持来完成。  下一级别是容器业务流程支持，该支持可为所选的特定业务流程协调程序添加相应的支持文件。  

借助 Visual Studio 2017，可以将 Docker Compose 和 Service Fabric 用作容器业务流程服务。  如果安装 [Visual Studio Tools for Kubernetes](https://aka.ms/get-vsk8stools)，则也可以使用 Kubernetes。

> [!NOTE]
> 如果使用的是 15.8 之前的 Visual Studio 2017 版本或使用的是 .NET Framework 项目模板（而不是 .NET Core），则在添加 Docker 支持时，会使用 Docker Compose 自动添加业务流程支持。 在 Visual Studio 2017 版本 15.0 到 15.7 中通过 Docker Compose 自动添加容器业务流程支持，并且该支持适用于 .NET Framework 项目。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="prerequisites"></a>系统必备

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)   
* 用于使用 .NET Core 2.2 进行开发的 [.NET Core 2.2 开发工具](https://dotnet.microsoft.com/download/dotnet-core/2.2)
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="docker-support-in-visual-studio"></a>Visual Studio 中的 Docker 支持

Docker 支持适用于 ASP.NET 项目、ASP.NET Core 项目，以及 .NET Core 和 .NET Framework 控制台项目。

Visual Studio 中的 Docker 支持因版本而异，以响应客户需求。 可以向项目添加两个级别的 Docker 支持，并且受支持的选项因项目类型和 Visual Studio 版本而异。 借助某些受支持的项目类型，如果只想将容器用于单个项目，而不使用业务流程，则可以通过添加 Docker 支持来完成。  下一级别是容器业务流程支持，该支持可为所选的特定业务流程协调程序添加相应的支持文件。  


借助 Visual Studio 2019，可以将 Docker Compose、Kubernetes 和 Service Fabric 用作容器业务流程服务。

> [!NOTE]
> 如果使用的是完整的 .NET Framework 控制台项目模板，则在添加 Docker 支持时，会自动添加使用 Docker Compose 的业务流程支持。
::: moniker-end

### <a name="adding-docker-support"></a>添加 Docker 支持

可以通过在创建新项目时选择“启用 Docker 支持”来在项目创建期间启用 Docker 支持，如以下屏幕截图所示  ：

::: moniker range="vs-2017"
![在 Visual Studio 中为新的 ASP.NET Core Web 应用启用 Docker 支持](./media/overview/enable-docker-support-visual-studio.png)
::: moniker-end
::: moniker range=">=vs-2019"
![在 Visual Studio 中为新的 ASP.NET Core Web 应用启用 Docker 支持](./media/overview/vs-2019/enable-docker-support-visual-studio.png)
::: moniker-end

> [!NOTE]
> 对于 .NET Framework 项目（而不是 .NET Core），只有 Windows 容器可用。

可以通过在“解决方案资源管理器”  中选择“添加”   > “Docker 支持”  来向现有项目添加 Docker 支持。 Add > Docker Support  和 Add > Container Orchestrator Support  命令位于“解决方案资源管理器”  中 ASP.NET Core 项目的项目节点的右键单击菜单（或上下文菜单）上，如以下屏幕截图所示：

![Visual Studio 中的“添加 Docker 支持”菜单选项](./media/overview/add-docker-support-menu.png)

当添加或启用 Docker 支持时，Visual Studio 会向项目添加以下各项：

- Dockerfile  文件
- .dockerignore 文件
- 对 Microsoft.VisualStudio.Azure.Containers.Tools.Targets 的 NuGet 包引用

::: moniker range=">=vs-2019"
添加 Docker 支持后，解决方案如下所示：

![包含 Dockerfile 和 .dockerignore 文件的解决方案资源管理器的屏幕截图](media/overview/vs-2019/dockerfile-dockerignore.png)
::: moniker-end

::: moniker range="vs-2017"
> [!NOTE]
> 当按以下屏幕截图所示在项目创建期间为 ASP.NET 项目（.NET Framework，而不是 .NET Core 项目）启用 Docker 支持时，还会添加容器业务流程支持。

![为 ASP.NET 项目启用 Docker Compose 支持](media/overview/enable-docker-compose-support.png)
::: moniker-end

## <a name="docker-compose-support"></a>Docker Compose 支持

当你想要使用 Docker Compose 撰写多容器解决方案时，请向项目添加容器业务流程支持。 这样就可以同时运行和调试一组容器（整个解决方案或项目组）（如果已在同一个 docker-compose.yml  文件中定义这些容器）。

若要使用 Docker Compose 添加容器业务流程支持，请右键单击“解决方案资源管理器”  中的解决方案或项目节点，然后选择“添加”>“容器业务流程支持”  。 然后，选择“Docker Compose”  以管理容器。

向项目添加容器业务流程支持后，会看到添加到项目的 Dockerfile  （如果尚无）以及添加到“解决方案资源管理器”  中的某个解决方案的 docker-compose  文件夹，如下所示：

![Visual Studio 解决方案资源管理器中的 Docker 文件](media/overview/docker-support-solution-explorer.png)

如果 docker-compose.yml  已存在，Visual Studio 只需向其添加配置代码所需的行。

对要使用 Docker Compose 控制的其他项目重复该过程。

## <a name="kubernetes-support"></a>Kubernetes 支持

::: moniker range="vs-2017"
若要添加 Kubernetes 支持，请安装 [Visual Studio Tools for Kubernetes](https://aka.ms/get-vsk8stools)。
::: moniker-end

借助 Kubernetes 支持，可以在本地项目和 [Azure Kubernetes 服务 (AKS)](/azure/aks) 中运行的 Kubernetes 群集之间启用连接，从而使用 Visual Studio 修改和调试 AKS 中运行的服务。  此服务由 [Azure Dev Spaces](/azure/dev-spaces/quickstart-netcore-visualstudio) 提供。 通过 Azure Dev Spaces，还可以设置名为 dev spaces  的 Kubernetes 服务的单独分支用于开发目的，因此可以有效地将生产服务与开发中的工作版本隔离，并使每个修改完全不同。

若要向项目添加 Kubernetes 支持，请在添加容器业务流程支持时选择“Kubernetes/Helm”  。 多个文件添加到项目，其中包括 azds.yaml  （用于配置 Azure Dev Spaces）和 Helm 图表（用于描述 Kubernetes 服务的结构）。

## <a name="service-fabric-support"></a>Service Fabric 支持

借助 Visual Studio 中的 Service Fabric 工具，可以开发和调试 Azure Service Fabric、进行本地运行和调试并部署到 Azure。

::: moniker range="vs-2017"
安装了 Azure 开发工作负载的 Visual Studio 2017 版本 15.9 及更高版本支持使用 Windows 容器和 Service Fabric 业务流程来开发容器化微服务。
::: moniker-end
::: moniker range=">=vs-2019"
Visual Studio 2019 支持使用 Windows 容器和 Service Fabric 业务流程来开发容器化微服务。
::: moniker-end

有关详细教程，请参阅[教程：将 Windows 容器中的 .NET 应用程序部署到 Azure Service Fabric](/azure/service-fabric/service-fabric-host-app-in-a-container)。

有关 Azure Service Fabric 的详细信息，请参阅 [Service Fabric](/azure/service-fabric)。

## <a name="continuous-delivery-and-continuous-integration-cicd"></a>持续交付和持续集成 (CI/CD)

Visual Studio 与 Azure Pipelines 轻松集成，以便自动完成服务代码和配置更改的持续集成和交付。 若要开始使用，请参阅[创建第一个管道](/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)。

有关 Service Fabric 的信息，请参阅[教程：使用 Azure DevOps Projects 将 ASP.NET Core 应用部署到 Azure Service Fabric](/azure/devops-project/azure-devops-project-service-fabric)。

有关 Kubernetes 的信息，请参阅[将 Docker 容器应用部署到 Azure Kubernetes 服务](/azure/devops/pipelines/apps/cd/deploy-aks?view=azure-devops)。

## <a name="next-steps"></a>后续步骤

有关服务实现以及将 Visual Studio 工具用于容器的更多详细信息，请阅读以下文章：

[Debugging apps in a local Docker container](edit-and-refresh.md)（在本地 Docker 容器中调试应用）

[使用 Visual Studio 将 ASP.NET 容器部署到容器注册表](hosting-web-apps-in-docker.md)
