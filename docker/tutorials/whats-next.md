---
title: Docker 教程 - 后续内容
description: 介绍使用云原生计算基础项目通过编排扩展 Docker 应用的选项。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: f93185641a0814797b66eae90714e04cac83f7e5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176661"
---
# <a name="whats-next"></a>后续步骤

虽然你已经完成了教程，但仍然有很多关于容器的知识需要学习！
我们不会在这里深入探讨，但下面将介绍一些其他方面！

## <a name="container-orchestration"></a>容器业务流程

在生产环境中运行容器非常困难。 你不希望登录到计算机，并直接运行 `docker run` 或 `docker-compose up`。 为什么看不到？ 如果容器出现故障，会发生什么情况呢？ 如何跨多台计算机进行缩放？ 容器编排解决了这一问题。 Kubernetes、Swarm、Nomad 和 AKS 等工具都可帮助解决此问题，但方法略有不同。

通常情况下，你会设置“管理员”来接收“预期状态”。 此状态可能是“我想要运行 Web 应用的两个实例并公开端口 80”。 然后，管理员查看群集中的所有计算机，并将工作委托给“辅助角色”节点。 管理员查看更改（如容器退出），然后进行处理以使“实际状态”反映预期状态。

## <a name="cloud-native-computing-foundation-projects"></a>云原生计算基础项目

CNCF 独立于供应商，适合各种开放源代码项目，包括 Kubernetes、Prometheus、Envoy、Linkerd、NAT 等！ 可[在此处查看成熟和孵化项目](https://www.cncf.io/projects/)，[在此处查看整个 CNCF 布局](https://landscape.cncf.io/)。 有很多项目可帮助解决监视、日志记录、安全性、映像注册表、消息传送等方面的问题！

如果你对容器布局和云原生应用程序开发还不熟悉，欢迎使用！ 请连接到社区，提出问题并保持学习！ 我们非常高兴你能加入！

## <a name="working-with-docker-in-vs-code"></a>使用 VS Code 中的 Docker

了解有关使用 VS Code Docker 扩展的详细信息：

- [VS Code Docker 扩展概述](https://code.visualstudio.com/docs/containers/overview)
- [Node.js 入门](https://code.visualstudio.com/docs/containers/quickstart-node)
- [Python 入门](https://code.visualstudio.com/docs/containers/quickstart-python)
- [.NET Core 入门](https://code.visualstudio.com/docs/containers/quickstart-aspnet-core)
- [调试容器化应用](https://code.visualstudio.com/docs/containers/debug-common)
