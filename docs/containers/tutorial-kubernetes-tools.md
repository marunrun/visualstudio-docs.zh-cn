---
title: Kubernetes 工具教程 | Microsoft Docs
ms.date: 06/08/2018
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.workload:
- azure
ms.openlocfilehash: 931f8c2a6d3be130ef78f59f9b3853d28fad8cd4
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444682"
---
# <a name="get-started-with-visual-studio-kubernetes-tools"></a>Visual Studio Kubernetes 工具入门

Visual Studio Kubernetes 工具有助于简化面向 Kubernetes 的容器化应用程序的开发。 Visual Studio 可以自动创建支持 Kubernetes 部署所需的配置即代码文件，如 Dockerfile 和 Helm 图表。 可使用 Azure Dev Spaces 在实时 Azure Kubernetes 服务 (AKS) 群集中调试代码，或从 Visual Studio 内部直接发布到 AKS 群集。

本教程介绍如何使用 Visual Studio 将 Kubernetes 支持添加到项目并将其发布到 AKS。 如果主要需求是使用 [Azure Dev Spaces](/azure/dev-spaces/) 来调试和测试 AKS 中运行的项目，则可以改为转到 [Azure Dev Spaces 教程](/azure/dev-spaces/get-started-netcore-visualstudio)。

## <a name="prerequisites"></a>必备条件

若要利用此新的功能，将需要以下各项：

::: moniker range="vs-2017"
- 带有“ASP.NET 和 Web 开发”工作负载的最新版本 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)  。
- [适用于 Visual Studio的 Kubernetes 工具](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-tools-for-kubernetes)，可作为单独的下载提供。
::: moniker-end
::: moniker range="vs-2019"
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) 与“ASP.NET 和 Web 开发”工作负载  。
::: moniker-end
- 在开发工作站（即运行 Visual Studio 的位置）上安装的 [Docker Desktop](https://store.docker.com/editions/community/docker-ce-desktop-windows)，如果要生成 Docker 映像，请调试本地运行的 Docker 容器，或发布到 AKS。 （使用 Azure Dev Spaces 在 AKS 中生成和调试 Docker 容器时不需要 Docker  。）
::: moniker range="vs-2017"
- 若要从 Visual Studio 发布到 AKS（使用 Azure Dev Spaces 在 AKS 中进行调试不需要）  ：

    1. [AKS 发布工具](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-tools-for-kubernetes)，可作为单独的下载提供。

    1. 一个 Azure Kubernetes 服务群集。 有关详细信息，请参阅[创建 AKS 群集](/azure/aks/kubernetes-walkthrough-portal#create-an-aks-cluster)。 确保从开发工作站[连接到群集](/azure/aks/kubernetes-walkthrough#connect-to-the-cluster)。

    1. 已在开发工作站上安装 Helm CLI。 有关详细信息，请参阅 [Installing Helm](https://github.com/helm/helm-www/blob/master/content/en/docs/helm/helm_install.md)（安装 Helm）。

    1. 使用 `helm init` 命令针对 AKS 群集配置的 Helm。 有关如何执行此操作的详细信息，请参阅[如何配置 Helm](/azure/aks/kubernetes-helm#configure-helm)。
::: moniker-end

## <a name="create-a-new-kubernetes-project"></a>创建新的 Kubernetes 项目

::: moniker range="vs-2017"

安装适当的工具后，启动 Visual Studio 并新建项目。 在“云”下，选择“适用于 Kubernetes 的容器应用程序”项目类型   。 选择此项目类型，然后选择“确定”  。

![新建 Kubernetes 应用项目的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-new-k8s-app.png)

::: moniker-end
::: moniker range=">= vs-2019"

在 Visual Studio“开始”窗口中，搜索 Kubernetes，然后选择“适用于 Kubernetes 的容器应用程序”   。

![新建 Kubernetes 应用项目的屏幕截图](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-new-k8s-app1.png)

提供项目名称。

![新建 Kubernetes 应用项目的屏幕截图](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-new-k8s-app2.png)

::: moniker-end

然后可选择要创建的 ASP.NET Core Web 应用的类型。 选择“Web 应用程序”  。 此对话框中不显示常用的“启用 Docker 支持”选项  。  默认为适用于 Kubernetes 的容器应用程序启用 Docker 支持。

::: moniker range="vs-2017"

![Web 应用选择的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-web-app-selection-screen.png)

::: moniker-end
::: moniker range=">=vs-2019"

![Web 应用选择的屏幕截图](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-web-app-selection-screen-2019.png)

::: moniker-end

## <a name="add-kubernetes-support-to-an-existing-project"></a>将 Kubernetes 支持添加到现有项目

或者可将 Kubernetes 支持添加到现有 ASP.NET Core web 应用程序项目。 为此，请右键单击该项目，然后选择“添加” **“容器业务流程协调程序支持”**  >   。

::: moniker range="vs-2017"

![添加容器业务流程协调程序菜单项的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-add-container-orchestrator.png)

::: moniker-end
::: moniker range=">=vs-2019"

![添加容器业务流程协调程序菜单项的屏幕截图](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-add-container-orchestrator-2019.png)

::: moniker-end

在对话框中，选择 "Kubernetes/Helm"，然后选择“确定”   。

![添加容器业务流程协调程序对话框的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-add-container-orchestrator-dialog-box.PNG)

## <a name="what-visual-studio-creates-for-you"></a>Visual Studio 为你创建的内容

在新建“适用于 Kubernetes 的容器应用程序”项目或向现有项目添加 Kubernetes 容器业务流程协调程序支持后，项目中会显示一些其他文件，可以帮助你部署到 Kubernetes  。

::: moniker range="vs-2017"

![添加容器业务流程协调程序支持后解决方案资源管理器的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-solution-explorer.png)

::: moniker-end
::: moniker range="vs-2019"

![添加容器业务流程协调程序支持后解决方案资源管理器的屏幕截图](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-solution-explorer-2019.png)

::: moniker-end

添加的文件包括：

- Dockerfile，使你能够生成托管此 Web 应用程序的 Docker 容器映像。 如你所见，在调试并部署到 Kubernetes 时，Visual Studio 工具会利用此 Dockerfile。 如果希望直接使用 Docker 映像，可以右键单击 Dockerfile，然后选择“生成 Docker 映像”  。

   ![生成 Docker 映像选项的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-build-docker-image.png)

- Helm 图表，及 charts 文件夹  。 这些 yaml 文件构成应用程序的 Helm 图表，可用于将其部署到 Kubernetes。 有关 Helm 的详细信息，请参阅 [https://www.helm.sh](https://www.helm.sh)。

- azds.yaml  . 这包含 Azure Dev Spaces 的设置，可在 Azure Kubernetes 服务中提供快速的迭代调试体验。 有关详细信息，请参阅 [Azure Dev Spaces 文档](/azure/dev-spaces/azure-dev-spaces)。

::: moniker range="vs-2017"

## <a name="publish-to-azure-kubernetes-service-aks"></a>发布到 Azure Kubernetes 服务 (AKS)

所有这些文件都准备就绪后，如往常一样，可使用 Visual Studio IDE 来编写和调试应用程序代码。 还可使用 [Azure Dev Spaces](/azure/dev-spaces/) 来快速地运行和调试 AKS 群集中实时运行的代码。 有关详细信息，请参阅 [Azure Dev Spaces 教程](/azure/dev-spaces/get-started-netcore-visualstudio)

使用所需方式运行代码后，可直接从 Visual Studio 发布到 AKS 群集。

若要执行此操作，首先需要仔细检查是否已按照[先决条件](#prerequisites)部分所述，在发布到 AKS 的项下安装所有内容，并运行链接中提供的所有命令行步骤。 然后，设置发布配置文件，使其将容器映像发布到 Azure 容器注册表 (ACR)。 AKS 随后可从 ACR 拉取容器映像并将其部署到群集中。

1. 在解决方案资源管理器中，右键单击项目，选择“发布”    。

   ![“发布”菜单项的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-publish-project.png)

2. 在“发布”屏幕中，对于发布目标，选择“容器注册表”，然后按照提示选择容器注册表   。 如果还没有容器注册表，请选择“新建 Azure 容器注册表”，从 Visual Studio 创建容器注册表  。 有关详细信息，请参阅[将容器发布到 Azure 容器注册表](hosting-web-apps-in-docker.md)。

   ![“选取发布目标”屏幕的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-publish-to-acr.png)

3. 返回解决方案资源管理器中，右键单击解决方案，然后单击“发布到 Azure AKS”   。

   ![“发布到 Azure AKS”菜单项的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-publish-solution.png)

4. 选择订阅和 AKS 群集，以及刚刚创建的 ACR 发布配置文件。 然后单击“确定”  。

   ![“发布到 AKS”屏幕的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-publish-to-aks.png)

   这会转到“发布到 Azure AKS”屏幕  。

5. 选择“配置 Helm”链接，可更新用于在服务器上安装 Helm 图表的命令行  。

   ![“配置 Helm 链接”的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-configure-helm.png)

   如有需要指定的自定义命令行参数（例如其他 Kubernetes 上下文或图表名称），则更新命令行非常有用。

   ![“Helm 配置”屏幕的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-helm-configure-screen.png)

6. 准备好进行部署后，单击“发布”按钮，将应用程序发布到 AKS  。

   ![“发布到 Azure AKS”屏幕的屏幕截图](media/tutorial-kubernetes-tools/k8s-tools-publish-screen.png)

::: moniker-end

祝贺你！ 现可使用 Visual Studio 的全部功能来开发所有 Kubernetes 应用。

## <a name="next-steps"></a>后续步骤

阅读 [AKS 文档](/azure/aks)，深入了解如何在 Azure 上进行 Kubernetes 开发。

阅读 [Azure Dev Spaces 文档](/azure/dev-spaces/)，深入了解 Azure Dev Spaces
