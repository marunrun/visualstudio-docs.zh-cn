---
title: 在 Azure 虚拟机上使用 Visual Studio
titleSuffix: ''
description: 了解如何在 Azure 虚拟机上使用 Visual Studio
ms.date: 11/17/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- azure services
- virtual machine
- installation
- visual studio
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: f73a410752d4b3befd00602f84d575a040c457fe
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850450"
---
# <a name="visual-studio-images-on-azure"></a><a id="top"> </a> Azure 上的 Visual Studio 映像

使用预配置的 Azure 虚拟机 (VM) 中的 Visual Studio 是从零构建开发环境的一种简单快速的方法。 具有不同 Visual Studio 配置的系统映像位于 [Azure 市场](https://azuremarketplace.microsoft.com/marketplace/apps/category/compute?filters=virtual-machine-images%3Bmicrosoft%3Bwindows&page=1&subcategories=application-infrastructure)。

不熟悉 Azure？ [创建免费的 Azure 帐户](https://azure.microsoft.com/free)。

## <a name="what-configurations-and-versions-are-available"></a>提供了哪些可用的配置和版本？

在 Azure 市场中，可以找到最新主版本（Visual Studio 2019、Visual Studio 2017 和 Visual Studio 2015）的映像。  对于发布的每个主版本，都可以看到最初的“发布到 Web”(RTW) 版本和最新更新版本。  其中每个版本都提供 Visual Studio Enterprise 和 Visual Studio Community 版本。  这些映像至少每个月更新一次，以包括最新的 Visual Studio 和 Windows 更新。  尽管映像的名称保持不变，但每个映像的说明包括已安装的产品版本和映像的截止日期。

| 发行版本                                                                                                                                          | 版本              |    产品版本    |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------:|:-----------------------:|
| [Visual Studio 2019：最新（版本 16.8）](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019latest?tab=Overview) | Enterprise、Community | 版本 16.8.0    |
| [Visual Studio 2019：RTW](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019?tab=Overview)                         | 企业            | 版本 16.0.20    |
| [Visual Studio 2017：最新（版本 15.9）](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)           | Enterprise、Community | 版本 15.9.29   |
| [Visual Studio 2017：RTW](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)                             | Enterprise、Community | 版本 15.0.28   |
| [Visual Studio 2015：最新（更新 3）](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio?tab=Overview)               | Enterprise、Community | 版本 14.0.25431.01 |

> [!NOTE]
> 根据 Microsoft 服务策略，Visual Studio 2015 最初发布的 (RTW) 版本已过期，无法提供服务。 Visual Studio 2015 Update 3 是为 Visual Studio 2015 产品线提供的唯一剩余版本。

有关详细信息，请参阅 [Visual Studio 维护策略](/visualstudio/productinfo/vs-servicing-vs)。

## <a name="what-features-are-installed"></a>安装了哪些功能？

每个映像都包含为该 Visual Studio 版本推荐的功能集。 通常，安装包括：

* 所有可用工作负荷，包括每个工作负荷推荐的可选组件
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

## <a name="what-size-vm-should-i-choose"></a>应选择什么大小的 VM？

Azure 提供各种虚拟机大小。 由于 Visual Studio 是一个功能强大的多线程应用程序，因此 VM 大小需要包含至少两个处理器和 7 GB 内存。 我们为 Visual Studio 映像建议以下 VM 大小：

* Standard_D2_v3
* Standard_D2s_v3
* Standard_D4_v3
* Standard_D4s_v3
* Standard_D2_v2
* Standard_D2S_v2
* Standard_D3_v2

有关最新虚拟机大小的详细信息，请参阅 [Azure 中的 Windows 虚拟机大小](/azure/virtual-machines/windows/sizes)。

使用 Azure，可通过调整 VM 大小来重新平衡初始选择。 可为新的 VM 预配更合适的大小，也可调整现有 VM 的大小，使其适应不同的底层硬件。 有关详细信息，请参阅[调整 Windows VM 大小](/azure/virtual-machines/windows/resize-vm)。

## <a name="after-the-vm-is-running-whats-next"></a>VM 运行后，下一步是什么？

Visual Studio 遵循 Azure 中的“自带许可”模式。 与专有硬件上的安装一样，第一步是授权 Visual Studio 安装。 若要解锁 Visual Studio，请执行以下任一操作：
- 使用与 Visual Studio 订阅关联的 Microsoft 帐户登录
- 使用最初购买附带的产品密钥解锁 Visual Studio

有关详细信息，请参阅[登录 Visual Studio](../ide/signing-in-to-visual-studio.md) 和[如何解锁 Visual Studio](../ide/how-to-unlock-visual-studio.md)。

## <a name="how-do-i-save-the-development-vm-for-future-or-team-use"></a>如何保存开发 VM 供将来使用或供团队使用？

开发环境的种类繁多，构建更复杂的环境需要付出实际成本。 不管环境如何配置，都可以将已配置的 VM 保存为或捕获为“基础映像”供将来使用或供团队的其他成员使用。 然后，启动新的 VM 时，从基础映像（而不是 Azure 市场映像）对其进行预配。

快速摘要：使用系统准备工具 (Sysprep) 关闭正在运行的 VM，然后通过 Azure 门户的 UI 将 VM 捕获为映像（图 1）。 Azure 会将包含该映像的 `.vhd` 文件保存在所选存储帐户中。 然后，新映像将在资源订阅列表中显示为映像资源。

![通过 Azure 门户 UI 捕获映像](media/capture-vm.png)

（图 1）通过 Azure 门户 UI 捕获映像。

有关详细信息，请参阅[在 Azure 中创建通用化 VM 的托管映像](/azure/virtual-machines/windows/capture-image-resource)。

> [!IMPORTANT]
> 不要忘记使用 Sysprep 来准备 VM。 如果缺少该步骤，Azure 无法从映像配置 VM。

> [!NOTE]
> 仍需花费一些成本来存储映像，但与从头开始重建 VM 的开销成本相比，对每个需要 VM 的团队成员而言，这种增量成本可能微不足道。 例如，创建和存储 127 GB 的映像每月只需几美元，整个团队都可重复使用该映像。 但是，与每位员工为构建和验证正确配置的开发箱以供个人使用而投入的时间相比，这些成本微不足道。

此外，开发任务或技术可能需要更大的规模，如各种开发配置和多种计算机配置。 可使用 Azure 开发测试实验室，创建可自动构造“黄金映像”的配方。 还可以使用开发测试实验室管理团队正在运行的 VM 策略。 [使用面向开发人员的 Azure 开发测试实验室](/azure/devtest-lab/devtest-lab-developer-lab)是获取有关开发测试实验室更多信息的最佳来源。

## <a name="next-steps"></a>后续步骤

了解预配置的 Visual Studio 映像后，下一步是创建新 VM：

* [通过 Azure 门户创建 VM](/azure/virtual-machines/windows/quick-create-portal)
* [Windows 虚拟机概述](/azure/virtual-machines/windows/overview)
