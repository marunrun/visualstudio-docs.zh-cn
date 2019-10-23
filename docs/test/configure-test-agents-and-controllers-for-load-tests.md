---
title: 为负载测试配置测试代理和测试控制器
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, test agents and controllers
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 657037cdb3ef36c4ef81c72cb4fc43f6a94203a3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665175"
---
# <a name="overview-of-test-agents-and-test-controllers-for-running-load-tests"></a>用于运行负载测试的测试代理和测试控制器的概述

Visual Studio 可以使用物理计算机或虚拟机为应用生成模拟负载。 这些机器必须由一个测试控制器和一个或多个测试代理组成。 可以使用测试控制器和测试代理生成超出一台计算机单机生成能力的负载。

> [!NOTE]
> 还可以使用基于云的负载测试来提供同时生成访问网站的多个用户的负载的虚拟机。 但是，不支持在云托管的虚拟机上使用测试控制器/测试代理安装程序。 在[使用 Azure Test Plans 运行负载测试](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts)中详细了解基于云的负载测试。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="load-simulation-architecture"></a>负载模拟体系结构

负载模拟体系结构包含 Visual Studio 客户端、测试控制器和测试代理。

- 客户端用于开发测试、运行测试，以及查看测试结果。

- 测试控制器用于管理测试代理和收集测试结果。

- 使用测试代理来运行测试并收集数据，包括系统信息和测试设置中定义的 ASP.NET 分析数据。

此体系结构提供了以下好处：

- 通过将其他测试代理添加到测试控制器增加负载生成的功能。

- 在相同或不同计算机上灵活安装客户端、测试控制器和测试代理软件。 例如:

   **本地配置：**

  - Machine1：Visual Studio、控制器、代理。

    ![使用控制器和代理的本地计算机](./media/load-test-configa.png)

    **典型远程配置：**

  - Machine1 and 2：Visual Studio（多名测试人员可以使用同一个控制器）。

  - Machine3：控制器（也可安装代理）。

  - Machine4-n：与 Machine3 上的控制器关联的一个或多个代理。

    ![使用控制器和代理的远程计算机](./media/load-test-configb.png)

即使测试控制器通常管理多个测试代理，代理也只能关联到一个控制器。 每个测试代理可以由一组开发人员共享。 此体系结构可以轻松地增加测试代理数量，从而生成更大的负载。

## <a name="test-agent-and-test-controller-interaction"></a>测试代理和测试控制器交互

测试控制器管理一组测试代理来运行测试。 测试控制器与测试代理进行通信，以启动测试、停止测试、跟踪测试代理状态和收集测试结果。

### <a name="test-controller"></a>测试控制器

测试控制器提供了运行测试的一般体系结构，并且包含运行负载测试的特殊功能。 测试控制器会将负载测试发送到所有的测试代理并等待，直到所有的测试代理都初始化该测试。 所有的测试代理准备就绪后，测试控制器会将消息发送到测试代理，以启动测试。

### <a name="test-agent"></a>测试代理

测试代理作为一种服务运行，它侦听来自测试控制器的请求以启动新的测试。 当测试代理收到请求时，测试代理服务将启动在其上运行测试的一个进程。 每个测试代理都运行相同的负载测试。

测试代理由管理员分配权重，并且根据测试代理的权重分配负载。 例如，如果测试代理 1 的权重为 30，测试代理 2 的权重为 70，而且负载设置为 1000 个用户，则测试代理 1 将模拟 300 个虚拟用户，而测试代理 2 将模拟 700 个虚拟用户。 请参阅[使用 Visual Studio 管理测试控制器和测试代理](../test/manage-test-controllers-and-test-agents.md)。

测试代理接受一组测试和一组模拟参数作为输入。 关键概念是测试独立于在其中运行它们的计算机。

## <a name="test-controller-and-test-agent-connection-points"></a>测试控制器和测试代理连接点

下图演示测试控制器、测试代理和客户端之间的连接点。 它概述了用于传入和传出连接的端口以及在这些端口上使用的安全限制。

![测试控制器和测试代理的端口和安全性](./media/test-controller-agent-firewall.png)

有关详细信息，请参阅[为测试控制器和测试代理配置端口](../test/configure-ports-for-test-controllers-and-test-agents.md)。

## <a name="test-controller-and-agent-installation-information"></a>测试控制器和代理安装信息

关于测试控制器和测试代理的硬件和软件要求，以及安装它们和配置你的环境以获得最佳性能的过程的重要信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

## <a name="use-the-test-controller-and-test-agent-with-unit-tests"></a>使用测试控制器和测试代理与单元测试

安装 Test Controller 以及一个或多个代理后，可以在负载测试的测试设置中指定是否对 Test Controller 使用远程执行。 此外，您可以指定在测试设置中与代理相关联的角色一起使用的数据和诊断适配器。

## <a name="see-also"></a>请参阅

- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)