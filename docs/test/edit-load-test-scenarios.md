---
title: 负载测试方案
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios
- load tests, user activities
- load tests, modeling scenarios
ms.assetid: fec04f2e-bf38-4d44-b2ec-fa50f58fd0d9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 647548a59c965b6feacb994efa041ecd5b6c6b91
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786157"
---
# <a name="edit-load-test-scenarios"></a>编辑负载测试方案

负载测试方案指定负载模式、测试组合、浏览器组合和网络组合。 方案非常重要，因为借助方案可以配置测试以模拟复杂真实的工作负载。

例如，你可能正在测试某电子商务网站点，其 Internet 前端由数百位并发客户同时访问，这些客户的访问连接速度和浏览器都各不相同。 该站点还可能具有管理功能，供内部员工用于更新产品和查看统计信息。 这些内部用户通常会使用相同的浏览器和高速 LAN 连接访问该站点。 你可能希望将这两种不同用户组的属性封装到不同方案中。 每个方案可包含一个虚拟用户类型。 在这种情况下，可生成一个负载测试方案来表示虚拟客户，生成另一个方案来表示网站的虚拟内部用户。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="scenario-components"></a>方案组件

创建负载测试时指定的任何初始配置选项和设置，之后都可在“负载测试编辑器”中进行修改。 还可以将新的方案、运行设置和计数器集添加到负载测试。

![负载测试方案](../test/media/loadtesteditinscenarios.png)

方案包含以下组件：

|术语|定义|
|-|-|
|浏览器组合|模拟虚拟用户通过各种 Web 浏览器访问网站的过程。|
|负载模式|指定负载测试期间的活动虚拟用户数和启动新用户的速率。 例如：单步负载、恒负载和基于目标的负载模式。|
|测试组合模型|指定虚拟用户在负载测试方案中运行给定测试的概率。 例如:20% 的概率运行 TestA，80% 的概率运行 TestB。 测试组合模型应反映特定方案的测试目标。|
|测试组合|测试组合是有关构成方案的 Web 性能测试和单元测试的选择以及这些测试的分布。|
|网络组合|模拟虚拟用户通过各种网络连接访问网站的过程。 网络组合提供的选项包括 LAN、电缆调制解调器和其他选项。|

方案具有可以使用“负载测试编辑器”进行编辑的多个其他属性。 有关详细信息，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

## <a name="tasks"></a>任务

|任务|相关主题|
|-|-----------------------|
|**在方案中添加人工交互暂停：** 思考时间用于模拟人类与网站执行的各种交互之间存在等待时间这种行为。 Web 性能测试中的各个请求之间以及负载测试方案的各个测试迭代之间均会产生思考时间。 在负载测试中使用思考时间对于创建更为精确的负载模拟很有用。|-   [编辑思考时间以模拟网站人工交互延迟](../test/edit-think-times-in-load-test-scenarios.md)|
|**为方案指定虚拟用户数：** 可以配置负载模式属性以指定在负载测试期间如何调整模拟的用户负载。 可获取三个内置负载模式：常量负载模式、分级负载模式和基于目标的负载模式。 根据负载测试目标，选择负载模式并将属性调整为适当的级别。|-   [编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)|
|**配置方案中运行测试的虚拟用户的概率：** 可使用测试组合指定虚拟用户在负载测试方案中运行指定测试的概率。 这样可以更逼真地模拟负载。 应用程序可以有多个工作流而不是只得有一个，这样可以更逼真地模拟最终用户与应用程序的交互方式。|-   [编辑文本组合模型](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)|
|**在负载测试方案中添加或删除 Web 性能或单元测试：** 可以在方案中的负载测试中添加或删除 Web 性能或单元测试。 一个负载测试可以包含一个或多个方案，每个方案又可以包含一个或多个 Web 性能测试或单元测试。|-   [编辑测试组合](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)|
|**为方案配置所需的网络组合：** 使用网络组合可以在负载测试方案中更真实地模拟网络负载。 负载是使用不同种类的网络类型组合生成的，而不仅仅是一种单一的网络类型。 这样可以更逼真地模拟最终用户与应用程序交互的方式。 网络组合模型应反映该方案的目标。|-   [指定虚拟网络类型](../test/specify-virtual-network-types-in-a-load-test-scenario.md)|
|**为方案选择适当的 Web 浏览器组合：** 使用浏览器组合可以在负载测试方案中更真实地模拟 Web 负载。 负载使用异类浏览器组合（而非单一种类的浏览器）生成。 这样便创建了一种与你的应用程序所用浏览器更为接近的浏览器使用情形。|-   [指定 Web 浏览器类型](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)|
|**为方案配置测试迭代设置：** 可以使用“负载测试编辑器”和“属性”窗口编辑负载测试方案，以配置测试迭代设置。 默认情况下，在设置方案时，不会设置最大测试迭代数。 你可以选择配置方案中的最大迭代数以及它们之间的暂停时间。|-   [为方案配置测试迭代](../test/configure-test-iterations-in-a-load-test-scenario.md)|
|**为方案配置延迟设置：** 使用“负载测试编辑器”和“属性”窗口，可以指定负载测试中开始某一方案前的延迟时间。 例如，如果需要一个方案开始生成另一个方案所使用的项，则可能希望使用“延迟开始时间”属性。 可延迟该要使用生成项的方案以使生成项的方案能填充某些数据。|-   [配置方案启动延迟](../test/configure-scenario-start-delays.md)|
|**指定要在负载测试方案中使用的远程计算机：** 在创建负载测试后，可以编辑负载测试方案的属性以指示要包括的测试代理。 有关详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。|-   [如何：指定要使用的测试代理](../test/how-to-specify-test-agents-to-use-in-load-test-scenarios.md)|

## <a name="see-also"></a>请参阅

- [编辑负载测试](../test/edit-load-tests.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)