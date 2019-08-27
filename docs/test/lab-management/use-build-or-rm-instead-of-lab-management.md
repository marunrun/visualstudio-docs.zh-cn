---
title: 使用 Azure Pipelines 进行自动化测试
ms.date: 10/19/2018
ms.topic: conceptual
helpviewer_keywords:
- automated testing, lab management, test lab
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: d9bb59a383db46fdfc3b7e5a9a2f429399630873
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952771"
---
# <a name="use-azure-test-plans-instead-of-lab-management-for-automated-testing"></a>使用 Azure Test Plans 代替实验室管理工具版进行自动测试

如果使用 Microsoft 测试管理器和实验室管理工具版进行自动测试或生成-部署-测试自动化，请参阅本主题，本主题介绍了如何使用 Azure Pipelines 和 Team Foundation Server (TFS) 中的[生成和发布](/azure/devops/pipelines/index?view=vsts)功能实现相同的目的。

## <a name="build-deploy-test-automation"></a>生成-部署-测试自动化

Microsoft 测试管理器和实验室管理工具版依赖 XAML 生成定义来自动生成、部署和测试应用程序。 XAML 生成依赖于在 Microsoft 测试管理器中创建的各种构造（例如实验室环境、测试套件和测试设置）和各种基础结构组件（例如生成控制器、生成代理、测试控制器和测试代理）来实现此目标。 可以使用 Azure Pipelines 或 TFS 以更少的步骤完成相同的操作。

| 步骤 | 使用 XAML 生成 | 在生成或发布中 |
|-------|----------------------|-----------------|
| 确定部署生成和运行测试的计算机。 | 使用这些计算机在 Microsoft 测试管理器中创建标准实验室环境。 | n/a |
| 确定要运行的测试。 | 在 Microsoft 测试管理器中创建测试套件、创建测试用例并将自动化与每个测试用例关联。 在 Microsoft 测试管理器中创建测试设置，标识计算机在测试应运行的实验室环境中的角色。 | 如果打算通过测试计划管理测试，则以相同的方式在 Microsoft 测试管理器中创建自动测试套件。 如果想从生成产生的测试二进制文件直接运行测试，则可以跳过此步骤。 两种情况下都无需创建测试设置。 |
| 自动部署和测试。 | 使用 LabDefaultTemplate.*.xaml 创建 XAML 生成定义。 在生成定义中指定生成、测试套件和实验室环境。 | 使用单一环境创建[生成或发布管道](/azure/devops/pipelines/index?view=vsts)。 使用命令行任务从 XAML 生成定义运行相同的部署脚本，并使用“测试代理部署”和“运行功能测试”任务运行自动测试。 将一系列计算机及其凭据指定为这些任务的输入。 |

此方案中使用 Azure Pipelines 或 TFS 的一些好处是：

* 不需要生成控制器或测试控制器。
* 生成或发布过程中会通过任务安装测试代理。
* 可以轻松地自定义部署步骤。 不再受到使用单一脚本的限制。 还可利用产品和 Visual Studio Marketplace 中提供的许多任务。
* 无需维护测试套件。 可从二进制文件直接运行测试。
* 每个生成或发布中运行的测试会提供更丰富的内联报告体验。
* 可以跟踪每个环境上当前部署和测试的资产类型（发布、生成、工作项、提交）。
* 可自定义和扩展自动化，并轻松部署到多个测试环境，甚至生产环境。
* 可计划在签入或提交时，或在每天的特定时间执行自动化操作。

## <a name="self-service-management-of-scvmm-environments"></a>SCVMM 环境的自助式管理

[Microsoft 测试管理器的测试中心](/azure/devops/test/mtm/guidance-mtm-usage?view=vsts)可以管理环境模板库，并使用 [SCVMM 服务器](/system-center/vmm/overview?view=sc-vmm-1801)根据需要配置环境。

实验室中心的自助式预配功能有两个不同的目标：

* 通过更简单的方法来管理基础结构。 举例来说，基础结构管理包括管理 VM 模板和环境模板，以及自动创建专用网络，以将克隆环境相互隔离。

* 让团队能够通过更简单的方法在其测试和部署活动中使用虚拟机。 举例来说，简单的使用方式包括使实验室环境可通过同一项目安全模型进行访问，在测试方案中以集成方式使用这些虚拟机。

但是，虽然随着时代发展现已具有更丰富的公有和私有云管理系统，例如 [Microsoft Azure](https://azure.microsoft.com/) 和 [Microsoft Azure Stack](https://azure.microsoft.com/overview/azure-stack/)，但 TFS 2017 和更高版本中的基础结构管理功能仍然没有变化。 相反，关注的问题仍然是如何方便地使用此类云基础结构管理的资源。

下表总结了在实验室中心执行的典型活动，以及如何通过 SCVMM 或 Azure（适用于基础结构管理活动）或通过 TFS 和 Azure DevOps Services（适用于测试或部署活动）完成这些活动：

| 步骤 | 使用实验室中心 | 在生成或发布中 |
|-------|-----------------|-----------------------|
| 管理环境模板库。 | 创建实验室环境。 在虚拟机上安装必要的软件。 进行系统准备，并将环境存储为库中的模板。 | 使用 SCVMM 管理控制台直接创建和管理虚拟机模板或服务模板。 使用 Azure 时，选择其中的一个 [Azure 快速入门模板](https://azure.microsoft.com/resources/templates/)。 |
| 创建实验室环境。 | 在库中选择一个环境模板并部署该模板。 提供自定义虚拟机配置所需的参数。 | 使用 SCVMM 管理控制台根据模板直接创建虚拟机或服务实例。 使用 Azure 门户直接创建资源。 或使用环境创建发布定义。 使用 Azure 任务或 [SCVMM 集成扩展](https://marketplace.visualstudio.com/items?itemname=ms-vscs-rm.scvmmapp)中的任务创建新虚拟机。 创建此定义的新发布相当于在实验室中心中创建新环境。 |
| 连接到计算机。 | 在“环境查看器”中打开实验室环境。 | 使用 SCVMM 管理控制台直接连接到虚拟机。 或者使用虚拟机的 IP 地址或 DNS 名称打开远程桌面会话。 |
| 执行环境的检查点，或将环境还原到干净的检查点。 | 在“环境查看器”中打开实验室环境。 选择执行检查点或还原到之前的检查点的选项。 | 使用 SCVMM 管理控制台直接对虚拟机执行这些操作。 或者若要在更大的自动化过程中执行这些步骤，则在发布定义的环境中包括 [SCVMM 集成扩展](https://marketplace.visualstudio.com/items?itemname=ms-vscs-rm.scvmmapp)中的检查点任务。 |

## <a name="create-network-isolated-environments"></a>创建已隔离网络的环境

网络隔离实验室环境是一系列 SCVMM 虚拟机，这些虚拟机可以在不引起网络冲突的情况下进行安全克隆。 根据使用一组网络接口卡在专用网络中配置虚拟机和使用另一组网络接口卡在公用网络中配置虚拟机的一系列说明，在 MTM 中完成此操作。

但是，Azure Pipelines 和 TFS 与 SCVMM 生成和部署任务结合起来，即可用于管理 SCVMM 环境、预配隔离虚拟网络和实现生成-部署-测试方案。 例如，可执行任务以：

* 创建、还原和删除检查点
* 基于模板创建新的虚拟机
* 启动和停止虚拟机
* 针对 SCVMM 运行自定义 PowerShell 脚本

详情请参阅[创建用于生成-部署-测试方案的虚拟网络隔离环境](/azure/devops/pipelines/targets/create-virtual-network?view=vsts)。
