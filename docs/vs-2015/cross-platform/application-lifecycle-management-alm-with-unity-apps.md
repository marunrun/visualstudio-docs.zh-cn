---
title: 适用于 Unity 应用的应用程序生命周期管理 (ALM) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 2dc61e63-9ba2-4c16-b1ad-f46249e576b6
caps.latest.revision: 14
author: conceptdev
ms.author: crdun
manager: jillfra
ms.openlocfilehash: 364f98fd991494ae83f6175289f34832e271159b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300039"
---
# <a name="application-lifecycle-management-alm-with-unity-apps"></a>适用于 Unity 应用的 Visual Studio 应用程序生命周期管理 (ALM)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

开发适用于现代平台的应用涉及许多活动，并不仅仅只是编写代码。 这些活动被称为 DevOps（开发+操作），它们跨越应用的整个生命周期，包括计划和跟踪工作、设计和实现代码、管理源代码存储库、运行生成、管理持续集成和部署、测试（包括单元测试和 UI 测试）、在开发和生产环境中运行各种形式的诊断以及通过遥测和分析实时监控应用的性能和用户行为。  
  
 Visual Studio、Visual Studio Team Services 和 Team Foundation Server 提供了各种 DevOps 功能，也被称为应用程序生命周期管理或 ALM。 其中许多都适用于跨平台项目，包括采用 Unity 创建的游戏和沉浸式图形应用 - 特别是在将 C# 用作脚本语言时。 但是，由于 Unity 具有其自己的开发环境和运行时引擎，大量的 ALM 功能并不能像适用于在 Visual Studio 中生成的其他项目一样适用。  
  
 下表标识了在使用 Unity 时，Visual Studio ALM 功能的适用或不适用情况。 请参阅链接文档，获取功能自身的详细信息。  
  
## <a name="agile-tools"></a>敏捷工具  
 参考链接： **[工作](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)** （使用 Visual Studio Team Services 或 TFS，包括 Team Explorer Everywhere）  
  
 常规注释：所有的计划和跟踪功能均独立于项目类型和编码语言。  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|管理积压工作和冲刺 (sprint)|是||  
|跟踪工作|是||  
|团队聊天室协作|是||  
|看板|是||  
|报告和可视化进度|是||  
  
## <a name="modeling"></a>建模  
 参考链接： **[体系结构分析和建模](../modeling/analyze-and-model-your-architecture.md)**  
  
 概述：虽然这些设计功能既不依赖于编码语言，也不使用 C# 等 .NET 语言，但它们是在具有对象层次结构和类关系的传统应用程序范例上运行。 在 Unity 中设计游戏会同时涉及到不同的范例，即图形对象、声音、着色器、脚本等关系。 因此，Visual Studio 建模关系图工具并非专用于 Unity 项目。 它们可能被用于管理 C# 脚本内的关系，而这也只是其部分应用范围。  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|序列图|No||  
|依赖项关系图|No||  
|调用层次结构|No||  
|类设计器|No||  
|体系结构资源管理器|No||  
|UML 关系图（用例、活动、类、组件、序列和 DSL）|No||  
|层关系图|No||  
|层验证|No||  
  
## <a name="code"></a>代码  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|[使用 Team Foundation 版本控制](https://msdn.microsoft.com/library/1d629052-c65d-4c5d-81eb-eaa4413fe285)或 Visual Studio Team Services|是|Unity项目是一个文件集合，可以像任何其他项目一样放置到版本控制系统中，但有几点需要特别注意，请参见此表后内容。|  
|[Team Services 中的 Git 入门](https://msdn.microsoft.com/library/32f46ecd-1b03-4ef0-a9c4-8a120da2b03f)|是|请参阅表后的注释。|  
|[代码分析/提高代码质量（引用、建议的更改等）](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)|是||  
|[查找代码更改和其他历史记录](../ide/find-code-changes-and-other-history-with-codelens.md)|是||  
|[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)|是||  
  
 Unity 版本控制特别注意事项：  
  
1. Unity 使用一个默认隐藏的不透明库来追踪和游戏资产相关的元数据。 若要使文件和元数据保持同步，需使元数据可见，并将其保存在更易于管理的区块中。 有关详细信息，请参阅 [Using External Version Control Systems with Unity](https://docs.unity3d.com/Manual/ExternalVersionControlSystemSupport.html)（配合使用 Unity 与外部版本控制系统）（Unity 文档）。  
  
2. 并非 Unity 项目中的所有文件和文件夹都适合实施源代码管理，上面的链接中也给予了说明。 应添加 Assets 和 ProjectSettings 文件夹，但不应添加 Library 和 Temp 文件夹。 有关不会执行源代码管理的生成的文件的附加列表，请参阅 StackOverflow 上的讨论[如何使用 Git 进行 Unity3D 源代码管理？](https://stackoverflow.com/questions/18225126/how-to-use-git-for-unity3d-source-control)。 许多开发人员都针对此主题发表了博文。  
  
3. Unity 项目中的二进制资产 — 例如纹理或音频文件 — 可能会占用大量存储空间。 Git 等各种源代码管理系统会为每一次更改保留一份唯一副本，即使更改仅影响文件的一小部分。 这会导致 Git 存储库变得臃肿。 为解决此问题，Unity 开发人员通常选择仅将最终资产添加到其存储库中，并使用另一种方法来保留其资产的工作历史记录，例如 OneDrive、DropBox 或 git-annex。 这种方法有效，因为这种资产通常无需随源代码更改而进行版本控制。 开发人员通常也将项目编辑器的资产序列化模式设置为强制文本，以便以文本格式保存场景文件，而不是允许在源代码管理中进行合并的二进制格式。 有关详细信息，请参阅 [Editor Settings](https://docs.unity3d.com/Manual/class-EditorManager.html)（编辑器设置）（Unity 文档）。  
  
## <a name="build"></a>生成  
 参考链接： **[生成](/azure/devops/pipelines/index)**  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|本地 TFS 服务器|可能|Unity 项目通过 Unity 环境生成，而不是 Visual Studio 生成系统（在 Visual Studio Tools 中为 Unity 生成项目将对脚本进行编译，但不是会生成可执行文件）。 可以[从命令行生成 Unity 项目](https://docs.unity3d.com/Manual/CommandLineArguments.html)（Unity 文档），因此用户可以在 TFS 服务器上配置 MSBuild 进程，以执行相应的 Unity 命令，前提是该计算机已经安装了 Unity。<br /><br /> Unity 也提供 [Unity 云生成](https://build.cloud.unity3d.com/landing/)，它会监视 Git 或 SVN 储存库，并定期运行生成。 目前它并不适用于 Team Foundation 版本控制或 Visual Studio Team Services。|  
|链接到 Visual Studio Team Services 的本地生成服务器|可能|给定上述相同条件，更有可能指向通过 Visual Studio Team Services 触发的生成，以便使用本地 TFS 计算机。  有关说明，请参阅[生成服务器](https://msdn.microsoft.com/library/2d258a0a-f178-4e93-9da1-eba61151af3c)。|  
|Visual Studio Team Services 承载的控制器服务|No|目前不支持 Unity 生成。|  
|生成带有前脚本和后脚本的定义|是|使用 Unity 命令行运行生成的自定义生成定义还可以配置为预生成和后生成脚本。|  
|包括封闭签入的持续集成|是|仅在 Git 用于拉取请求（而非签入）时，封闭签入才适用于 TFVC。|  
  
## <a name="testing"></a>正在测试  
 参考链接： **[测试应用程序](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)**  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|规划测试、创建测试用例和组织测试套件|是||  
|手动测试|是||  
|测试管理器（记录和播放测试）|仅限 Windows 设备和 Android 模拟器||  
|代码覆盖率|不可用|Unity 内进行单元测试时以及不是 Visual Studio 时不适用，请参阅下文。|  
|[单元测试代码](../test/unit-test-your-code.md)|在 Unity 中，但不在 Visual Studio 中|Unity 提供了自己的单元测试框架作为 [Unity 测试工具](https://www.assetstore.unity3d.com/en/#!/content/13802)（Unity 资产商店）的一部分。 单元测试结果在 Unity 中报告，将不会出现在 Visual Studio 内。|  
|[使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)|No|编码的 UI 测试依赖于应用 UI 中可读取的控件；Unity 应用程序在本质上都是图形，因此编码的 UI 测试工具无法读取其内容。|  
  
## <a name="improve-code-quality"></a>提高代码质量  
 参考链接： **[提高代码质量](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)**  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|[分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|是|可以在 Visual Studio 中分析 C# 脚本代码。|  
|[使用代码克隆检测功能查找重复代码](https://msdn.microsoft.com/library/a97cd5a6-5ffa-4104-9627-8e59e513654d)|是|可以在 Visual Studio 中分析 C# 脚本代码。|  
|[测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|是|可以在 Visual Studio 中分析 C# 脚本代码。|  
|[性能资源管理器](../profiling/performance-explorer.md)|No|使用 [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html)（Unity 网站）。|  
|[分析 .NET Framework 内存问题](../misc/analyze-dotnet-framework-memory-issues.md)|No|Visual Studio 工具不具有进入 Mono 框架（用于 Unity）进行探查的挂钩。 使用 [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html)（Unity 文档）。|  
  
## <a name="release-management"></a>发布管理  
 参考链接： **[使用发布管理来自动进行部署](https://msdn.microsoft.com/library/vs/alm/release/overview)**  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|管理发布进程|是||  
|部署到服务器以通过脚本进行侧载|是||  
|上载到应用商店|Partial|提供了一些扩展，这些扩展可使某些应用商店的此进程自动化。  请参阅 [Visual Studio Team Services 的扩展](https://marketplace.visualstudio.com/VSTS)；例如，[Google Play 的扩展](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play)。|  
  
## <a name="monitor-with-hockeyapp"></a>使用 HockeyApp 进行监控  
 参考链接： **[使用 HockeyApp 进行监控](https://www.hockeyapp.net/features/)**  
  
|功能|通过 Unity 提供支持|其他注释|  
|-------------|--------------------------|-------------------------|  
|崩溃分析、遥测和 beta 版本分发|是|HockeyApp 主要用于处理 beta 版本分发和获取崩溃报告。<br /><br /> 对于 C# 脚本中的遥测，可以使用任何分析框架，前提是它运行在 Unity 使用的 .NET 版本上。 但是，这仅允许在游戏脚本内进行分析，而无法深入到 Unity 引擎内部。 目前，没有任何适用于 Application Insights 的插件，但有适用于其他分析解决方案的插件，例如 [Unity Analytics](https://www.assetstore.unity3d.com/en/#!/content/28120)和 [Google Analytics](https://github.com/googleanalytics/google-analytics-plugin-for-unity)。 当然，Unity Analytics 等服务由于理解 Unity 项目的本质，可提供比一般框架有意义的多的分析。|
