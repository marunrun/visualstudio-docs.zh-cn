---
title: 在 Visual Studio 中使用 Local Process with Kubernetes（预览版）
ms.technology: vs-azure
ms.date: 06/02/2020
ms.topic: conceptual
description: 了解如何在 Visual Studio 中使用 Local Process with Kubernetes 将开发计算机连接到 Kubernetes 群集
keywords: Local Process with Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, 容器
monikerRange: '>=vs-2019'
ms.openlocfilehash: b057670f60554a066356ad34525f0276d8dc826c
ms.sourcegitcommit: 510a928153470e2f96ef28b808f1d038506cce0c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86454350"
---
# <a name="use-local-process-with-kubernetes-preview"></a>使用 Local Process with Kubernetes（预览版）

通过 Local Process with Kubernetes，你可在开发计算机上运行和调试代码，同时 Kubernetes 群集与其余应用程序或服务仍然保持连接。 例如，如果你有一个包含许多相互依赖的服务和数据库的大型微服务体系结构，则在开发计算机上复制这些依赖项可能会很困难。 此外，在内部循环开发期间，针对每次代码更改生成代码并将其部署到 Kubernetes 群集可能会缓慢、耗时且难以与调试程序一起使用。

Local Process with Kubernetes 可直接在开发计算机与群集之间创建连接，从而避免生成代码并将其部署到群集。 通过在调试时将开发计算机连接到群集，可以在完整应用程序的上下文中快速测试和开发服务，而无需创建任何 Docker 或 Kubernetes 配置。

Local Process with Kubernetes 将重定向已连接的 Kubernetes 群集与开发计算机之间的流量。 此流量重定向允许开发计算机上的代码与 Kubernetes 群集中运行的服务进行通信，就像它们位于同一个 Kubernetes 群集中一样。 Local Process with Kubernetes 还提供了一种方法来复制开发计算机中可用于 Kubernetes 群集中 pod 的环境变量和已装载的卷。 允许访问开发计算机上的环境变量和已装载卷，可以快速处理代码而无需手动复制这些依赖项。

本指南将介绍如何使用 Local Process with Kubernetes 来重定向 Kubernetes 群集与开发计算机上运行的代码之间的流量。 本指南还提供了一个脚本，用于在 Kubernetes 群集上部署包含多个微服务的大型示例应用程序。

> [!IMPORTANT]
> 此功能目前处于预览状态。 需同意[补充使用条款][preview-terms]才可使用预览版。 在正式版 (GA) 推出之前，此功能的某些方面可能会有所更改。

## <a name="before-you-begin"></a>在开始之前

本指南使用[共享单车示例应用程序][bike-sharing-github]演示如何将开发计算机连接到 Kubernetes 群集。 如果你已在 Kubernetes 群集上运行自己的应用程序，仍可以执行以下步骤，使用你自己的服务名称。

### <a name="prerequisites"></a>先决条件

* Azure 订阅。 如果没有 Azure 订阅，可以创建一个[免费帐户](https://azure.microsoft.com/free)。
* [已安装 Azure CLI][azure-cli]。
* 在 Windows 10 上运行 [Visual Studio 2019][visual-studio] 版本 16.7 预览版 4 或更高版本，并且已安装 Azure 开发工作负载。
* [已安装 Local Process for Kubernetes 扩展][lpk-extension]。

此外，对于 .NET 控制台应用程序，请安装 Microsoft.VisualStudio.Azure.Kubernetes.Tools.Targets NuGet 包。

## <a name="create-a-kubernetes-cluster"></a>创建 Kubernetes 群集

在[支持的区域][supported-regions]中创建 AKS 群集。 以下命令创建名为 *MyResourceGroup* 的资源组，以及名为 *MyAKS* 的 AKS 群集。

```azurecli-interactive
az group create \
    --name MyResourceGroup \
    --location eastus

az aks create \
    --resource-group MyResourceGroup \
    --name MyAKS \
    --location eastus \
    --node-count 3 \
    --generate-ssh-keys
```

## <a name="install-the-sample-application"></a>安装示例应用程序

使用提供的脚本在群集上安装示例应用程序。 可使用 [Azure Cloud Shell][azure-cloud-shell] 运行该脚本。

```azurecli-interactive
git clone https://github.com/Microsoft/mindaro
cd mindaro
chmod +x ./local-process-quickstart.sh
./local-process-quickstart.sh -g MyResourceGroup -n MyAKS
```

通过打开其公共 URL（显示在安装脚本的输出中），导航到运行群集的示例应用程序。

```console
$ ./local-process-quickstart.sh -g MyResourceGroup -n MyAKS
Defaulting Dev spaces repository root to current directory : ~/mindaro
Setting the Kube context
...
To try out the app, open the url:
bikeapp.bikesharingweb.EXTERNAL_IP.nip.io
```

在上面的示例中，公共 URL 为 `bikeapp.bikesharingweb.EXTERNAL_IP.nip.io`。

## <a name="connect-to-your-cluster-and-debug-a-service"></a>连接到群集并调试服务

在开发计算机上，下载并配置 Kubernetes CLI 以使用 [az aks get-credentials][az-aks-get-credentials] 连接到 Kubernetes 群集。

```azurecli
az aks get-credentials --resource-group MyResourceGroup --name MyAKS
```

在 Visual Studio 中从[共享单车示例应用程序][bike-sharing-github]打开 mindaro/samples/BikeSharingApp/ReservationEngine/app.csproj。

在项目中，从启动设置下拉列表中选择“Local Process with Kubernetes”，如下所示。

![选择 Local Process with Kubernetes](media/local-process-kubernetes/choose-local-process.png)

单击 Local Process with Kubernetes 旁边的启动按钮。 在 Local Process with Kubernetes 对话框中：

* 选择订阅。
* 选择 MyAKS 作为群集。
* 选择 dev 作为命名空间。
* 选择 reservationengine 作为要重定向的服务。
* 选择应用作为启动配置文件。
* 选择 `http://bikeapp.bikesharingweb.EXTERNAL_IP.nip.io` 作为启动浏览器的 URL。

![选择 Local Process with Kubernetes 群集](media/local-process-kubernetes/choose-local-process-cluster.png)

> [!IMPORTANT]
> 只能重定向仅有一个 pod 的服务。

单击“保存并启动调试”。

将 Kubernetes 群集中 reservationengine 服务的所有流量重定向到开发计算机中运行的应用程序版本。 Local Process with Kubernetes 还会将应用程序的所有出站流量路由回 Kubernetes 群集。

> [!NOTE]
> 系统将提示你允许 KubernetesDNSManager 在提升特权下运行并修改主机文件。

当状态栏显示你已连接到 reservationengine 服务时，你的开发计算机已连接。

![已连接开发计算机](media/local-process-kubernetes/development-computer-connected.png)

> [!NOTE]
> 在后续启动时，不会显示 Local Process with Kubernetes 对话框来提示你。 可在项目属性的“调试”窗格中更新这些设置。

连接开发计算机后，流量将开始重定向到你要替换的服务的开发计算机。

## <a name="set-a-break-point"></a>设置断点

打开 [BikesHelper.cs][bikeshelper-cs-breakpoint] 并单击第 26 行的某处，以将光标置于该处。 若要设置断点，请按 F9，或者依次单击“调试”、“切换断点”  。

通过打开公共 URL 导航到示例应用程序。 选择“Aurelia Briggs (客户)”作为用户，然后选择要租赁的自行车。 单击“租赁自行车”。 返回 Visual Studio，将会看到第 26 行已突出显示。 你设置的断点已在第 26 行暂停了服务。 若要恢复服务，请按 *F5*，或者依次单击“调试”、“继续”。  返回到浏览器并验证页面是否显示你已租赁该自行车。

通过将光标置于 `BikesHelper.cs` 中的第 26 行并点击 F9 来删除断点。

> [!NOTE]
> 默认情况下，停止调试任务也会断开开发计算机与 Kubernetes 群集的连接。 你可以更改此行为，方法是在调试选项的“Kubernetes 调试工具”部分，将“调试后断开连接”改为“false”  。 更新此设置后，在停止并启动调试时，开发计算机将保持连接状态。 若要断开开发计算机与群集的连接，请单击工具栏上的“断开连接”按钮。
>
> 如果 Visual Studio 突然结束与群集的连接或终止，则在与 Local Process with Kubernetes 连接之前，你要重定向的服务可能不会还原为其原始状态。 若要解决此问题，请参阅[故障排除指南][troubleshooting]。

## <a name="using-logging-and-diagnostics"></a>使用日志记录和诊断

可在[开发计算机的 TEMP 目录][azds-tmp-dir]的 `Azure Dev Spaces` 目录中查找诊断日志。

## <a name="remove-the-sample-application-from-your-cluster"></a>从群集中删除示例应用程序

使用提供的脚本从群集中删除示例应用程序。

```azurecli-interactive
./local-process-quickstart.sh -c -g MyResourceGroup -n MyAKS
```

## <a name="next-steps"></a>后续步骤

了解 Local Process Kubernetes 的工作原理。

> [!div class="nextstepaction"]
> [Local Process with Kubernetes 的工作原理](overview-local-process-kubernetes.md)

[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[azds-vs-code]: https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-lates
[azure-cloud-shell]: /azure/cloud-shell/w.md
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials
[az-aks-vs-code]: https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-aks-tools
[bike-sharing-github]: https://github.com/Microsoft/mindaro
[preview-terms]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[bikeshelper-cs-breakpoint]: https://github.com/Microsoft/mindaro/blob/master/samples/BikeSharingApp/ReservationEngine/BikesHelper.cs#L26
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[visual-studio]: https://www.visualstudio.com/vs/
[lpk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro