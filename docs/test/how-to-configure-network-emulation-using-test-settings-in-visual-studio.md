---
title: 使用测试设置配置网络仿真
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, network emulation
ms.assetid: ff275cfb-5df9-4710-9a91-9caabaaad34f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c4738caa4fac8596db5b92c6cafa1c0f370e0363
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979401"
---
# <a name="how-to-configure-network-emulation-using-test-settings-in-visual-studio"></a>如何：在 Visual Studio 中使用测试设置配置网络仿真

可将诊断数据适配器配置为在 Visual Studio 中的各种网络环境下测试应用程序。 运行测试时，还可以将它配置为测试人工网络负载或瓶颈。

> [!WARNING]
> 如果运行测试的实际网络是比要仿真的网络速度慢的网络类型，则仍将以慢速网络运行测试。 仿真只会降低而不会加快网络环境的速度。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

下面的过程介绍如何通过配置编辑器配置网络仿真。 这些步骤同时适用于 Microsoft 测试管理器和 Visual Studio 中的配置编辑器。

> [!NOTE]
> 此网络仿真诊断数据适配器仅适用于 Visual Studio 测试设置。 不适用于 Microsoft 测试管理器中的测试设置。

必须将具有管理员特权的帐户用于网络仿真。 如果为运行手动测试的本地角色选择了网络仿真，则必须使用管理员特权启动 Microsoft 测试管理器。 如果对任意其他角色选择了网络仿真，则必须验证该角色计算机上的测试代理使用的用户帐户是否为管理员组的成员。 有关如何为测试代理设置帐户的详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

> [!NOTE]
> Network Service 帐户（测试代理的默认帐户）不是管理员组的成员。

**真实网络仿真**

Visual Studio 对所有测试类型使用基于软件的真实网络仿真。 这包括负载测试。 真实网络仿真通过直接操作网络数据包来模拟各种网络情况。 真实网络仿真程序通过使用可靠的物理链接（如以太网）可模拟有线和无线网络的行为。 下列网络特性加入到了真实网络仿真中：

- 通过网络的往返时间（延迟）

- 可用带宽量

- 排队行为

- 数据包丢失

- 数据包的重新排序

- 错误传播。

真实网络仿真还提供在基于 IP 地址或协议（如 TCP、UDP 和 ICMP）筛选网络数据包方面的灵活性。

基于网络的开发人员和测试人员可以使用真实网络仿真来模拟所需的测试环境，评估性能，预测更改的影响或做出有关技术优化的决策。 与硬件测试台相比，真实网络仿真是一个更廉价、更灵活的解决方案。

## <a name="configure-network-emulation-for-your-test-settings"></a>为测试设置配置网络仿真

在执行本过程中的步骤之前，必须从 Visual Studio 中打开测试设置，然后选择“数据和诊断”页。

### <a name="to-configure-network-emulation-for-your-test-settings"></a>为测试设置配置网络仿真

1. 选择用于仿真特定网络的角色。

    > [!NOTE]
    > 仅需对客户端角色或服务器角色配置网络仿真适配器。 无需对这两种角色都使用适配器。 适配器会模拟影响这两个角色之间的通信的网络噪音，因此不必对这两个角色都使用适配器。 除非必要，应为网络仿真适配器选取客户端角色，以避免服务器角色上的额外开销。

2. 选择“网络仿真”，然后选择“配置”。

     此时将显示配置网络仿真的对话框。

3. 选择“选择要使用的网络配置文件”旁边的箭头，然后选择要在运行测试时模拟的网络类型（例如“Cable-DSL 768Kps”）。

    > [!WARNING]
    > 如果运行测试的实际网络是比要仿真的网络速度慢的网络类型，则仍将以慢速网络运行测试。 仿真只会降低而不会加快网络环境的速度。

4. 如果测试设置中包括网络仿真诊断数据适配器并且打算在本地计算机中使用它，那么还必须将网络仿真驱动程序绑定到计算机的网络适配器之一。 必须具有网络仿真驱动程序，网络仿真诊断数据适配器才能起作用。 网络仿真驱动程序以两种方式安装和绑定到适配器：

    - **与 Microsoft Visual Studio 测试代理一起安装的网络仿真驱动程序：** Microsoft Visual Studio 测试代理可用于远程计算机和本地计算机。 安装 Visual Studio Test Agent 时，安装过程包含一个将网络仿真驱动程序绑定到网卡的配置步骤。 有关详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

    - **与 Microsoft Visual Studio Test Professional 一起安装的网络仿真驱动程序：** 第一次使用网络仿真时，系统会提示将网络仿真驱动程序绑定到网卡上。

    > [!TIP]
    > 也可以使用以下命令在不安装 Visual Studio 测试代理的情况下从本地计算机上的命令行中安装网络仿真驱动程序：**VSTestConfig NETWORKEMULATION /install**

## <a name="see-also"></a>请参阅

- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)
- [运行手动测试 (Azure Test Plans)](/azure/devops/test/run-manual-tests?view=vsts)