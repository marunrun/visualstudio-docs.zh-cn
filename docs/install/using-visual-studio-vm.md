---
title: 在 Azure 虚拟机上使用 Visual Studio
titleSuffix: ''
description: 了解如何在 Azure 虚拟机上使用 Visual Studio
ms.date: 12/06/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- azure services
- virtual machine
- installation
- visual studio
author: PhilLee-MSFT
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: dc5fc9642401b1c90f079cae714fca9e214d6d9c
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2019
ms.locfileid: "74903847"
---
# <a id="top"> </a> Azure 上的 Visual Studio 映像

使用预配置的 Azure 虚拟机 (VM) 中的 Visual Studio 是从零构建开发环境的一种简单快速的方法。 [Azure 市场](https://azuremarketplace.microsoft.com/marketplace/apps/category/compute?filters=virtual-machine-images%3Bmicrosoft%3Bwindows&page=1&subcategories=application-infrastructure) 中提供了具有不同 Visual Studio 配置的系统映像。

初次使用 Azure？ [创建免费的 Azure 帐户](https://azure.microsoft.com/free)。

## <a name="what-configurations-and-versions-are-available"></a>提供了哪些可用的配置和版本？

在 Azure 市场中，可以找到最新主版本的映像：Visual Studio 2019、Visual Studio 2017 和 Visual Studio 2015。  对于每个发布的主版本，可以看到最初“发布到 Web”(RTW) 版本和最新更新的版本。  其中每个版本都提供 Visual Studio Enterprise 和 Visual Studio Community 版本。  这些映像至少每月更新一次，以包含最新的 Visual Studio 和 Windows 更新。  映像的名称保持不变，但每个映像的说明将包含已安装的产品版本和映像的“截至”日期。

| 发行版本                                                                                                                                          | 版本              |    产品版本    |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------:|:-----------------------:|
| [Visual Studio 2019：最新（版本 16.4）](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019latest?tab=Overview) | Enterprise，Community | 版本 16.4.0    |
| [Visual Studio 2019：RTW](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019?tab=Overview)                         | 企业            | 版本 16.0.9    |
| [Visual Studio 2017：最新（版本 15.9）](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)           | Enterprise，Community | 版本 15.9.17   |
| [Visual Studio 2017：RTW](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)                             | Enterprise，Community | 版本 15.0.27   |
| [Visual Studio 2015：最新（更新 3）](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)               | Enterprise，Community | 版本 14.0.25431.01 |

> [!NOTE]
> 根据 Microsoft 服务策略，最初发布的 (RTW) Visual Studio 2015 版本已过维护期限。 Visual Studio 2015 Update 3 是 Visual Studio 2015 产品系列仅剩的版本。

有关详细信息，请参阅 [Visual Studio 服务策略](/visualstudio/productinfo/vs-servicing-vs)。

## <a name="what-features-are-installed"></a>安装了哪些功能？

每个映像都包含针对该 Visual Studio 版本的建议功能集。 通常情况下，安装包括：

* 所有可用的工作负载，包括每个工作负载的建议可选组件
* .NET 4.6.2 和 .NET 4.7 SDK、目标包和开发人员工具
* Visual F#
* 适用于 Visual Studio 的 GitHub 扩展
* LINQ to SQL 工具

在生成映像时，我们使用以下命令行来安装 Visual Studio：

```shell
    vs_enterprise.exe --allWorkloads --includeRecommended --passive ^
       --add Microsoft.Net.Component.4.7.SDK ^
       --add Microsoft.Net.Component.4.7.TargetingPack ^
       --add Microsoft.Net.Component.4.6.2.SDK ^
       --add Microsoft.Net.Component.4.6.2.TargetingPack ^
       --add Microsoft.Net.ComponentGroup.4.7.DeveloperTools ^
       --add Microsoft.VisualStudio.Component.FSharp ^
       --add Component.GitHub.VisualStudio ^
       --add Microsoft.VisualStudio.Component.LinqToSql
```

如果映像不包含所需的 Visual Studio 功能，请通过页面右上角的反馈工具提供反馈。

## <a name="what-size-vm-should-i-choose"></a>我应该选择哪种大小的 VM？

Azure 提供一系列完整的虚拟机大小。 因为 Visual Studio 是一个功能强大的多线程应用程序，所以需要至少包含 2 个处理器和 7 GB 内存的 VM 大小。 建议 Visual Studio 映像采用下列 VM 大小：

* Standard_D2_v3
* Standard_D2s_v3
* Standard_D4_v3
* Standard_D4s_v3
* Standard_D2_v2
* Standard_D2S_v2
* Standard_D3_v2

有关最新虚拟机大小的详细信息，请参阅 [Azure 中的 Windows 虚拟机大小](/azure/virtual-machines/windows/sizes)。

在 Azure 中，可以通过调整 VM 的大小重新平衡最初的选择。 可以预配大小更为合适的新 VM，也可以根据不同的基础硬件调整现有 VM 的大小。 有关详细信息，请参阅[调整 Windows VM 大小](/azure/virtual-machines/windows/resize-vm)。

## <a name="after-the-vm-is-running-whats-next"></a>在 VM 运行后，接下来要做什么？

Visual Studio 在 Azure 中遵循“自带许可”模型。 与在专有硬件上的安装类似，第一步都包括许可 Visual Studio 安装。 要解锁 Visual Studio，可以：
- 使用与 Visual Studio 订阅关联的 Microsoft 帐户登录
- 使用最初购买时附带的产品密钥解锁 Visual Studio

有关详细信息，请参阅[登录到 Visual Studio](../ide/signing-in-to-visual-studio.md) 和[如何解锁 Visual Studio](../ide/how-to-unlock-visual-studio.md)。

## <a name="how-do-i-save-the-development-vm-for-future-or-team-use"></a>如何保存开发 VM 以供日后或团队使用？

开发环境的范围非常大，构建更为复杂的环境将产生高昂的成本。 无论环境配置如何，都可以将配置的 VM 保存或捕获为“基础映像”，以供将来使用或由团队其他成员使用。 然后，在启动新的 VM 时，从基础映像而不是从 Azure 市场映像对其进行预配。

概要：使用系统准备工具 (Sysprep) 并关闭正在运行的 VM，然后通过 Azure 门户的 UI 来捕获（图 1）VM 作为映像  。 Azure 将在你所选的存储帐户中保存包含映像的 `.vhd` 文件。 然后，新映像将在资源订阅列表中显示为映像资源。

![通过 Azure 门户 UI 捕获映像](media/capture-vm.png)

 （图 1）通过 Azure 门户 UI 捕获映像。

有关详细信息，请参阅[在 Azure 中创建通用化 VM 的托管映像](/azure/virtual-machines/windows/capture-image-resource)。

> [!IMPORTANT]
> 切记使用 Sysprep 来准备 VM。 如果遗漏该步骤，则 Azure 无法从映像预配 VM。

> [!NOTE]
> 存储映像仍会产生一定的费用，但与从头开始为需要 VM 的每个团队成员重新构建 VM 所产生的开销成本相比，增加的这点成本就无关紧要了。 例如，每月创建和存储 127 GB 的映像供整个团队重复使用需要几美元。 但是，与每个员工投入数小时构建和验证正确配置的开发框供其个人使用相比，这些成本微不足道。

此外，开发任务或技术可能需要更大的规模，例如各种开发配置和多个计算机配置。 可以使用 Azure 开发测试实验室来创建可自动构建“黄金映像”的方案  。 还可以使用开发测试实验室针对团队运行的 VM 管理策略。 [使用适用于开发人员的 Azure DevTest 实验室](/azure/devtest-lab/devtest-lab-developer-lab)是详细了解 Azure DevTest 实验室的最佳来源。

## <a name="next-steps"></a>后续步骤

现已了解有关预配置的 Visual Studio 映像的信息，下一步是创建新的 VM：

* [通过 Azure 门户创建 VM](/azure/virtual-machines/windows/quick-create-portal)
* [Windows 虚拟机概述](/azure/virtual-machines/windows/overview)
