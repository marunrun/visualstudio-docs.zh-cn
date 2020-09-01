---
title: Docker 教程-后续操作
description: 介绍使用云本机计算基础项目扩展 Docker 应用的选项。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: f93185641a0814797b66eae90714e04cac83f7e5
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176661"
---
# <a name="whats-next"></a>后续步骤

虽然您已经完成了本教程的学习，但仍有更多的知识来了解容器！
您不会深入探讨这里的内容，但还有其他几个方面需要注意。

## <a name="container-orchestration"></a>容器业务流程

在生产环境中运行容器非常困难。 您不希望登录到计算机，只需运行 `docker run` 或 `docker-compose up` 。 为什么看不到？ 嗯，如果容器片，会发生什么情况呢？ 如何跨多台计算机进行缩放？ 容器业务流程解决了这一问题。 Kubernetes、Swarm、Nomad 和 AKS 等工具都可帮助解决此问题。

一般情况是，您的 "经理" 接收到了 **预期状态**。 此状态可能是 "我想要运行 web 应用的两个实例并公开端口 80"。 然后，管理人员查看群集中的所有计算机，并将工作委托给 "worker" 节点。 管理器监视 (例如，容器退出) 然后工作，以使 **实际状态** 反映预期状态。

## <a name="cloud-native-computing-foundation-projects"></a>云本机计算基础项目

CNCF 是针对不同开源项目（包括 Kubernetes、Prometheus、Envoy、Linkerd、NAT 等）的特定于供应商的主页！ 可在此处查看 [分级和 incubated 的项目](https://www.cncf.io/projects/) ，并在 [此处](https://landscape.cncf.io/)查看整个 CNCF。 有很多项目可帮助解决有关监视、日志记录、安全性、映像注册表、消息传送等问题！

如果你不熟悉容器环境和云本机应用程序开发，欢迎使用！ 请连接到社区，提出问题并继续学习！ 我们非常高兴！

## <a name="working-with-docker-in-vs-code"></a>在 VS Code 中使用 Docker

了解有关使用 VS Code Docker 扩展的详细信息：

- [VS Code Docker 扩展概述](https://code.visualstudio.com/docs/containers/overview)
- [Node.js入门 ](https://code.visualstudio.com/docs/containers/quickstart-node)
- [Python 入门](https://code.visualstudio.com/docs/containers/quickstart-python)
- [.NET Core 入门](https://code.visualstudio.com/docs/containers/quickstart-aspnet-core)
- [调试容器化应用](https://code.visualstudio.com/docs/containers/debug-common)
