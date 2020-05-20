---
title: 负载测试对测试控制器和测试代理的要求
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- agents, requirements
- controllers, requirements
ms.assetid: 372d97ce-12e4-46a9-9863-da508adba68f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 39b174b0b134fdfdf26570565aa6aa756ba43c92
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75588637"
---
# <a name="test-controller-and-test-agent-requirements-for-load-testing"></a>负载测试对测试控制器和测试代理的要求

包括单元测试、Web 性能测试、负载测试和手动测试在内的多种测试类型集成到了 Visual Studio 中。 Visual Studio 使 Visual Studio 应用程序生命周期管理用户可以使用测试控制器和一个或多个代理在远程计算机上运行测试。 请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="hardware-and-software-requirements"></a>硬件和软件要求

测试控制器和测试代理计算机均具有特定的硬件和软件要求。 此外，如果你需要跨多种语言部署测试控制器和测试代理计算机，则必须计划如何支持这些语言。

### <a name="hardware-requirements"></a>硬件要求

下表演示对部署测试控制器和测试代理建议的硬件要求。

|**配置**|组件 |**CPU**|**HD**|**内存**|
|-|-------------------|-|------------|-|
|少于 500 个虚拟用户|测试代理|2.6 GHz|10 GB|2 GB|
|少于 1000 个虚拟用户|测试代理|双处理器，2.6 GHz|10 GB|2 GB|
|N x 1000 个虚拟用户|测试代理|扩展到 N 个代理，每个代理都具有双处理器 2.6 Ghz|10GB|2GB|
|在测试环境中 \< 30 台计算机。 这包括进行测试的代理和服务器。|测试控制器|2.6 GHz|||
|测试环境中的计算机数为 N x 30。 这包括进行测试的代理和服务器。|测试控制器|N 个 2.6 GHz 处理器|||

> [!NOTE]
> 不同测试之间的虚拟用户数会出现很大的变化。 这种变化的主要原因在于思考时间或用户延迟中的变化  。 有关详细信息，请参阅[编辑思考时间以模拟网站上的人机交互延迟](../test/edit-think-times-in-load-test-scenarios.md)。 在负载测试中，Web 测试通常更为有效，并且会产生比单元测试更多的负载。 上表中的数字对在典型 Web 应用程序上运行的、思考时间为 3 到 5 秒的 Web 测试有效。

此处提供的准则供你作为硬件计划的常规指导。 根据测试数据量和测试代理数的不同，测试性能会有较大区别。 对于测试代理，可用的 CPU 速度和内存将限制测试负载。 测试控制器需要更多的资源，具体取决于测试中涉及的测试代理数和数据量。

运行 Visual Studio 的服务器应该具有可靠的网络连接，其最小带宽为 1 Mbps，最大延迟为 350 毫秒。 测试代理和测试控制器之间不应有任何防火墙。 如果测试性能达不到你的预期要求，请考虑升级硬件配置。

### <a name="additional-hardware-considerations"></a>其他硬件注意事项

测试代理在测试控制器上生成大量数据，具体取决于测试持续时间和测试大小。 通常，应为每 24 小时的测试数据准备额外的 10 GB 硬盘存储空间。

除了此处建议的硬件，你应考虑为关键的服务器安装其他硬件，如冗余电源和冗余风扇。

### <a name="language-requirements"></a>语言要求

为避免混乱和简化操作，应配置测试控制器和测试代理以使用与计算机操作系统和 Team Foundation Server 相同的语言。 如果测试代理和测试控制器安装在不同的计算机上，必须将两者配置为使用相同的语言。 但是，你可以在使用英语的操作系统上安装另一种语言版本的 Visual Studio，前提是该语言与 Team Foundation Server 部署的语言相匹配。

## <a name="monitor-agent-resources"></a>监视代理资源

可以通过在测试期间观察执行和扩展的 QTAgent\*.exe 进程来监视代理计算机以确定它们的资源需求。 QTAgent\*.exe 进程上最常见的瓶颈是 CPU 使用率。  如果 CPU 使用率始终在 95% 以上，则表示该代理负载较重。 下一个常见瓶颈是内存使用量。 对于要求高的测试，监视这些资源可帮助确定是否应该增加计算机资源或以不同方式分配测试。

## <a name="see-also"></a>另请参阅

- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)
