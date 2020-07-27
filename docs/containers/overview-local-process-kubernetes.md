---
title: 如何通过本地进程使用 Kubernetes
ms.technology: vs-azure
ms.date: 06/02/2020
ms.topic: conceptual
description: 介绍如何使用 Local Process with Kubernetes 将开发计算机连接到 Kubernetes 群集
keywords: Local Process with Kubernetes, Docker, Kubernetes, Azure, 容器
monikerRange: '>=vs-2019'
ms.openlocfilehash: adde9d8ecab93bdb6f0aebbd74730ef60bd80cf6
ms.sourcegitcommit: 510a928153470e2f96ef28b808f1d038506cce0c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86454353"
---
# <a name="how-local-process-with-kubernetes-works"></a>如何通过本地进程使用 Kubernetes

通过 Local Process with Kubernetes，你可在开发计算机上运行和调试代码，同时 Kubernetes 群集与其余应用程序或服务仍然保持连接。 例如，如果你有一个包含许多相互依赖的服务和数据库的大型微服务体系结构，则在开发计算机上复制这些依赖项可能会很困难。 此外，在内部循环开发期间，针对每次代码更改生成代码并将其部署到 Kubernetes 群集可能会缓慢、耗时且难以与调试程序一起使用。

Local Process with Kubernetes 可直接在开发计算机与群集之间创建连接，从而避免生成代码并将其部署到群集。 通过在调试时将开发计算机连接到群集，可以在完整应用程序的上下文中快速测试和开发服务，而无需创建任何 Docker 或 Kubernetes 配置。

Local Process with Kubernetes 将重定向已连接的 Kubernetes 群集与开发计算机之间的流量。 此流量重定向允许开发计算机上的代码与 Kubernetes 群集中运行的服务进行通信，就像它们位于同一个 Kubernetes 群集中一样。 Local Process with Kubernetes 还提供了一种方法来复制开发计算机中可用于 Kubernetes 群集中 pod 的环境变量和已装载的卷。 允许访问开发计算机上的环境变量和已装载卷，可以快速处理代码而无需手动复制这些依赖项。

## <a name="using-local-process-with-kubernetes"></a>使用 Local Process with Kubernetes

若要在 Visual Studio 中使用 Local Process with Kubernetes，需要在 Windows 10 上运行 [Visual Studio 2019][visual-studio] 版本 16.7 预览版 4 或更高版本，并安装 ASP.NET 和 Web 开发工作负载及 [Local Process Kubernetes][lpk-extension] 扩展。 使用 Local Process with Kubernetes 建立与 Kubernetes 群集的连接时，可以选择将所有流量重定向到群集中的现有 pod，或将所有流量从群集中的现有 pod 重定向到开发计算机。

> [!NOTE]
> 使用 Local Process with Kubernetes 时，系统将提示你输入要重定向到开发计算机的服务的名称。 使用此选项可以方便地识别用于重定向的 pod。 Kubernetes 群集与开发计算机之间的所有重定向都适用于 pod。

当 Local Process with Kubernetes 建立与群集的连接时，它会执行以下操作：

* 提示你在群集上配置要替换的服务，在开发计算机上配置用于代码的端口，并将代码的启动任务配置为一次性操作。
* 将群集上 pod 中的容器替换为远程代理容器，它会将流量重定向到开发计算机。
* 在开发计算机上运行 [kubectl port-forward][kubectl-port-forward]，将流量从开发计算机转发到群集中运行的远程代理。
* 使用远程代理从群集收集环境信息。 此环境信息包括环境变量、可见服务、卷装载和机密装载。
* 在 Visual Studio 中设置环境，以便开发计算机上的服务可以访问相同变量，就像它在该群集上运行一样。  
* 更新主机文件，以将群集上的服务映射到开发计算机上的本地 IP 地址。 这些主机文件条目允许开发计算机上运行的代码向群集中运行的其他服务发出请求。 为更新主机文件，Local Process with Kubernetes 将在连接到群集时请求对开发计算机的管理员访问权限。
* 开始在开发计算机上运行和调试代码。 如有必要，Local Process with Kubernetes 将释放开发计算机上的所需端口，方法是停止当前正在使用这些端口的服务或进程。

建立与群集的连接后，可以在计算机上本机运行和调试代码，而无需容器化，并且代码可以直接与群集的其余部分交互。 在连接期间，远程代理接收的任何网络流量都将重定向到指定的本地端口，让本机运行的代码可以接受和处理该流量。 群集中的环境变量、卷和机密可供开发计算机上运行的代码使用。 此外，由于 Local Process with Kubernetes 将主机文件条目和端口转发添加到了开发人员计算机，你的代码可以使用群集中的服务名称向群集上运行的服务发送网络流量，将该流量转发到群集中正在运行的服务。 在整个连接期间，流量在开发计算机和群集之间路由。

## <a name="diagnostics-and-logging"></a>诊断和日志记录

使用 Local Process with Kubernetes 连接到群集时，会将群集中的诊断日志记录到开发计算机的[临时目录][azds-tmp-dir]。

## <a name="limitations"></a>限制

Local Process with Kubernetes 具有以下限制：

* Local Process with Kubernetes 将单个服务的流量重定向到开发计算机。 不能使用 Local Process with Kubernetes 同时重定向多个服务。
* 服务必须由单个 pod 支持，才能连接到该服务。 不能连接到具有多个 pod 的服务，例如具有副本的服务。
* 要使 Local Process with Kubernetes 成功连接，一个 pod 只能有一个容器在该 pod 中运行。 Local Process with Kubernetes 不能连接到具有附加容器（如服务网格注入的 sidecar 容器）的 pod 的服务。
* Local Process with Kubernetes 需要提升的权限才能在开发计算机上运行，以便编辑主机文件。

## <a name="next-steps"></a>后续步骤

若要开始使用 Local Process with Kubernetes 将本地开发计算机连接到群集，请参阅[使用 Local Process with Kubernetes](local-process-kubernetes.md)。

[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest
[local-process-kubernetes-vs]: local-process-kubernetes.md
[kubectl-port-forward]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
[visual-studio]: https://visualstudio.microsoft.com/downloads/
[lpk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro