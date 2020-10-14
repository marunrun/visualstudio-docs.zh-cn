---
title: 将 Kubernetes 桥接用于 Visual Studio
titleSuffix: ''
ms.technology: vs-azure
ms.date: 06/02/2020
ms.topic: how-to
description: 了解如何在 Visual Studio 中使用 Bridge to Kubernetes 将开发计算机连接到 Kubernetes 群集
keywords: Bridge to Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, 容器
monikerRange: '>=vs-2019'
ms.author: ghogen
author: ghogen
manager: jillfra
ms.openlocfilehash: 7bbeec2baab018ea770dbee60db507399ebeb745
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91860446"
---
# <a name="use-bridge-to-kubernetes"></a>使用 Bridge to Kubernetes

可以使用 Bridge to Kubernetes 来重定向 Kubernetes 群集与开发计算机上运行的代码之间的流量。 本指南还提供了一个脚本，用于在 Kubernetes 群集上部署包含多个微服务的大型示例应用程序。

## <a name="before-you-begin"></a>在开始之前

本指南使用[共享单车示例应用程序][bike-sharing-github]演示如何将开发计算机连接到 Kubernetes 群集。 如果你已在 Kubernetes 群集上运行自己的应用程序，仍可以执行以下步骤，使用你自己的服务名称。

### <a name="prerequisites"></a>先决条件

* Azure 订阅。 如果没有 Azure 订阅，可以创建一个[免费帐户](https://azure.microsoft.com/free)。
* [已安装 Azure CLI][azure-cli]。
* 在 Windows 10 上运行 [Visual Studio 2019][visual-studio] 版本 16.7 预览版 4 或更高版本，并且已安装 Azure 开发工作负载。
* [已安装 Bridge to Kubernetes 扩展][btk-extension]。

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
chmod +x ./bridge-quickstart.sh
./bridge-quickstart.sh -g MyResourceGroup -n MyAKS
```

通过打开其公共 URL（显示在安装脚本的输出中），导航到运行群集的示例应用程序。

```console
$ ./bridge-quickstart.sh -g MyResourceGroup -n MyAKS
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

在 GitHub 的[共享单车示例应用程序][bike-sharing-github]存储库中，使用绿色的“代码”按钮上的下拉列表并选择“在 Visual Studio 中打开”，以在本地克隆存储库，并在 Visual Studio 中打开该文件夹 。 然后，使用“文件” > 打开项目”，在“samples/BikeSharingApp/ReservationEngine”文件夹中打开 app.config 项目  。

在项目中，从启动设置下拉列表中选择“Bridge to Kubernetes”，如下所示。

![选择 Bridge to Kubernetes](media/bridge-to-kubernetes/choose-bridge-to-kubernetes.png)

单击 Bridge to Kubernetes 旁边的启动按钮。 在“为 Bridge to Kubernetes 创建配置文件”对话框中：

* 选择订阅。
* 选择 MyAKS 作为群集。
* 选择 bikeapp 作为命名空间。
* 选择 reservationengine 作为要重定向的服务。
* 选择应用作为启动配置文件。
* 选择 `http://bikeapp.bikesharingweb.EXTERNAL_IP.nip.io` 作为启动浏览器的 URL。

![选择 Bridge to Kubernetes 群集](media/bridge-to-kubernetes/choose-bridge-cluster2.png)

> [!IMPORTANT]
> 只能重定向仅有一个 pod 的服务。

选择是否在隔离模式下运行，这意味着使用该群集的其他用户不会受到更改的影响。 通过将请求路由到每个受影响的服务的副本，但正常路由所有其他流量，可以实现此隔离模式。 有关如何执行此操作的更多说明，请参阅 [Bridge to Kubernetes 的工作原理][btk-overview-routing]。

单击“保存并启动调试”。

将 Kubernetes 群集中 reservationengine 服务的所有流量重定向到开发计算机中运行的应用程序版本。 Bridge to Kubernetes 还会将应用程序的所有出站流量路由回 Kubernetes 群集。

> [!NOTE]
> 系统将提示你允许 EndpointManager 在提升的权限下运行并修改主机文件。

当状态栏显示你已连接到 `reservationengine` 服务时，你的开发计算机已连接。

![已连接开发计算机](media/bridge-to-kubernetes/development-computer-connected.png)

> [!NOTE]
> 在后续启动时，系统不会提示“创建 Bridge to Kubernetes 的配置文件”对话框。 可在项目属性的“调试”中更新这些设置。

连接开发计算机后，流量将开始重定向到你要替换的服务的开发计算机。

## <a name="set-a-break-point"></a>设置断点

打开 [BikesHelper.cs][bikeshelper-cs-breakpoint] 并单击第 26 行的某处，以将光标置于该处。 若要设置断点，请按 F9，或选择“调试” > “切换断点” 。

通过打开公共 URL 导航到示例应用程序。 选择“Aurelia Briggs (客户)”作为用户，然后选择要租赁的自行车。 选择“租赁自行车”。 返回 Visual Studio，将会看到第 26 行已突出显示。 你设置的断点已在第 26 行暂停了服务。 若要恢复服务，请按“F5”，或单击“调试” > “继续”  。 返回到浏览器并验证页面是否显示你已租赁该自行车。

通过将光标置于 `BikesHelper.cs` 中的第 26 行并点击 F9 来删除断点。

> [!NOTE]
> 默认情况下，停止调试任务也会断开开发计算机与 Kubernetes 群集的连接。 你可以更改此行为，方法是在调试选项的“Kubernetes 调试工具”部分中将“调试后断开连接”更改为 `false` 。 更新此设置后，在停止并启动调试时，开发计算机将保持连接状态。 若要断开开发计算机与群集的连接，请单击工具栏上的“断开连接”按钮。

## <a name="additional-configuration"></a>其他配置

Bridge to Kubernetes 可以处理路由流量和复制环境变量，无需任何其他配置。 如果需要下载已装载到 Kubernetes 群集中的容器的所有文件（例如 ConfigMap 文件），可以创建 `KubernetesLocalProcessConfig.yaml` 以将这些文件下载到开发计算机。 有关详细信息，请参阅[将 KubernetesLocalProcessConfig.yaml 用于 Bridge to Kubernetes 的附加配置][kubernetesLocalProcessConfig-yaml]。

## <a name="using-logging-and-diagnostics"></a>使用日志记录和诊断

可在开发计算机的 TEMP 目录的 `Bridge to Kubernetes` 目录中查找诊断日志。 

## <a name="remove-the-sample-application-from-your-cluster"></a>从群集中删除示例应用程序

使用提供的脚本从群集中删除示例应用程序。

```azurecli-interactive
./bridge-quickstart.sh -c -g MyResourceGroup -n MyAKS
```

## <a name="next-steps"></a>后续步骤

了解 Bridge to Kubernetes 的工作原理。

> [!div class="nextstepaction"]
> [Bridge to Kubernetes 的工作原理](overview-bridge-to-kubernetes.md)

[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-vs-code]: https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-lates&preserve-view=true
[azure-cloud-shell]: /azure/cloud-shell/overview.md
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest&preserve-view=true#az-aks-get-credentials
[az-aks-vs-code]: https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-aks-tools
[bike-sharing-github]: https://github.com/Microsoft/mindaro
[preview-terms]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[bikeshelper-cs-breakpoint]: https://github.com/Microsoft/mindaro/blob/master/samples/BikeSharingApp/ReservationEngine/BikesHelper.cs#L26
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[visual-studio]: https://www.visualstudio.com/vs/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation