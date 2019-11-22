---
title: 适用于 Xamarin 应用的应用程序生命周期管理 (ALM) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: ff978cc2-5a25-46d6-921b-e51adaa65992
caps.latest.revision: 16
ms.author: crdun
manager: crdun
ms.openlocfilehash: 1a0ea4f611c5312331fa0e2f2f467b4189778f30
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300026"
---
# <a name="application-lifecycle-management-alm-with-xamarin-apps"></a>适用于 Xamarin 应用的应用程序生命周期管理 (ALM)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

借助 Xamarin，你可以使用 C#、.NET 和 Visual Studio 生成面向 Android、iOS 和 Windows 的跨平台移动应用。 Xamarin 允许在平台间共享大部分代码，只有一小部分需要特定于平台。 有关 Xamarin 的详细信息，请参阅 [Visual Studio 和 Xamarin](../cross-platform/visual-studio-and-xamarin.md)。  
  
 开发适用于现代平台的应用涉及许多活动，并不仅仅只是编写代码。 这些活动被称为 DevOps（开发+操作），它们跨越应用的整个生命周期，包括计划和跟踪工作、设计和实现代码、管理源代码存储库、运行生成、管理持续集成和部署、测试（包括单元测试和 UI 测试）、在开发和生产环境中运行各种形式的诊断以及通过遥测和分析实时监控应用的性能和用户行为。  
  
 Visual Studio、Visual Studio Team Services 和 Team Foundation Server 提供了各种 DevOps 功能，也被称为应用程序生命周期管理或 ALM。 其中许多功能都完全适用于跨平台的项目。  
  
 对 Xamarin 应用尤其如此，因为它们利用 C# 和 .NET 生成，一些 ALM 工具就基于此而构建。 其他工具则需要与生成和运行时环境紧密集成。 由于 Xamarin 应用在非 Windows 平台上运行，并使用 .NET 的 Mono 实现，Xamari 为某些需求提供了专用工具。  
  
 下表标识了哪些 Visual Studio ALM 功能预期能与 Xamarin 项目很好地配合使用、哪些功能具有局限性。 请参阅链接文档，获取功能自身的详细信息。  
  
## <a name="agile-tools"></a>敏捷工具  
 参考链接： **[工作](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)** （使用 Visual Studio Team Services 或 TFS，包括 Team Explorer Everywhere）  
  
 常规注释：所有的计划和跟踪功能均独立于项目类型和编码语言。  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|管理积压工作和冲刺 (sprint)|是||  
|跟踪工作|是||  
|团队聊天室协作|是||  
|看板|是||  
|报告和可视化进度|是||  
  
## <a name="modeling"></a>建模  
 参考链接： **[体系结构分析和建模](../modeling/analyze-and-model-your-architecture.md)**  
  
 设计功能独立于编程语言，或与 C# 之类的.NET 语言配合使用。 有关与代码相关的方面，请参阅[体系结构关系图和建模图在软件开发中的角色](../modeling/scenario-change-your-design-using-visualization-and-modeling.md#ModelingDiagramsTools)。  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|序列图|是||  
|依赖项关系图|是||  
|调用层次结构|是||  
|类设计器|是||  
|体系结构资源管理器|是||  
|UML 关系图（用例、活动、类、组件、序列和 DSL）|是||  
|层关系图|是||  
|层验证|是||  
  
## <a name="code"></a>代码  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|[使用 Team Foundation 版本控制](https://msdn.microsoft.com/library/1d629052-c65d-4c5d-81eb-eaa4413fe285)或 Visual Studio Team Services|是||  
|[Team Services 中的 Git 入门](https://msdn.microsoft.com/library/32f46ecd-1b03-4ef0-a9c4-8a120da2b03f)|是||  
|[代码分析/提高代码质量（引用、建议的更改等）](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)|是||  
|[查找代码更改和其他历史记录](../ide/find-code-changes-and-other-history-with-codelens.md)|是|排除跨特定于平台的边界，在这些地方直到运行时才会对实现进行解析。|  
|[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)|是||  
  
## <a name="build"></a>生成  
 参考链接： **[生成](/azure/devops/pipelines/index)**  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|本地 TFS 服务器|是|生成计算机必须安装 Xamarin，并且能够链接到 OSX 计算机以生成适用于 iOS 的应用。 请参阅 [为 Xamarin 配置 TFS](https://docs.microsoft.com/azure/devops/repos/tfvc/overview?view=azure-devops) （Xamarin 网站）|  
|链接到 Visual Studio Team Services 的本地生成服务器|是|有关说明，请参阅[生成服务器](https://msdn.microsoft.com/library/2d258a0a-f178-4e93-9da1-eba61151af3c)。|  
|Visual Studio Team Services 承载的控制器服务|是|请参阅 [Build your Xamarin app](https://www.visualstudio.com/docs/build/apps/mobile/xamarin)（生成 Xamarin 应用）。|  
|生成带有前脚本和后脚本的定义|是||  
|包括封闭签入的持续集成|是|仅在 Git 用于拉取请求（而非签入）时，封闭签入才适用于 TFVC。|  
  
## <a name="testing"></a>正在测试  
 参考链接： **[测试应用程序](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)**  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|规划测试、创建测试用例和组织测试套件|是||  
|手动测试|是||  
|测试管理器（记录和播放测试）|是|仅限 Visual Studio 中的 Windows 设备和 Android 仿真器。 可使用 [Xamarin Test Recorder](https://www.xamarin.com/test-cloud/recorder)（Xamarin 测试记录器）记录所有设备。|  
|代码覆盖率|不可用||  
|[单元测试代码](../test/unit-test-your-code.md)|是|对于 Windows 和 Android 目标，可以使用内置的 MSTest 工具。 若要在 Windows、Android 和 iOS 上运行单元测试，Xamarin 建议使用 NUnit。 请参阅 [为 Xamarin 配置 TFS](https://docs.microsoft.com/azure/devops/repos/tfvc/overview?view=azure-devops) （Xamarin 网站）。|  
|[使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)|仅限 Windows|Visual Studio 的 UI 测试记录器仅用于 Windows。 有关所有平台，请参阅 [Xamarin Test Recorder](https://www.xamarin.com/test-cloud/recorder)（Xamarin 测试记录器）。|  
  
## <a name="improve-code-quality"></a>提高代码质量  
 参考链接： **[提高代码质量](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)**  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|[分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|是||  
|[使用代码克隆检测功能查找重复代码](https://msdn.microsoft.com/library/a97cd5a6-5ffa-4104-9627-8e59e513654d)|是||  
|[测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|是||  
|[性能资源管理器](../profiling/performance-explorer.md)|No|改用通过 Xamarin Studio 使用 [Xamarin 探查器](https://docs.microsoft.com/xamarin/cross-platform/deploy-test/) 。 请注意 Xamarin 探查器当前处于预览状态，并且尚不适用于 Windows 目标。|  
|[分析 .NET Framework 内存问题](../misc/analyze-dotnet-framework-memory-issues.md)|No|Visual Studio 工具没有深入 Mono 框架进行探查的挂钩。|  
  
## <a name="release-management"></a>发布管理  
 参考链接： **[使用发布管理来自动进行部署](https://msdn.microsoft.com/library/vs/alm/release/overview)**  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|管理发布进程|是||  
|部署到服务器以通过脚本进行侧载|是||  
|上载到应用商店|Partial|提供了一些扩展，这些扩展可使某些应用商店的此进程自动化。  请参阅 [Visual Studio Team Services 的扩展](https://marketplace.visualstudio.com/VSTS)；例如，[Google Play 的扩展](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play)。|  
  
## <a name="monitor-with-hockeyapp"></a>使用 HockeyApp 进行监控  
 参考链接： **[使用 HockeyApp 进行监控](https://www.hockeyapp.net/features/)**  
  
|功能|通过 Xamarin 提供支持|其他注释|  
|-------------|----------------------------|-------------------------|  
|崩溃分析、遥测和 beta 版本分发|是||
