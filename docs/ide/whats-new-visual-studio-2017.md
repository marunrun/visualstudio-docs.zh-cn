---
title: Visual Studio 2017 中的新增功能
titleSuffix: ''
description: 了解 Visual Studio 2017 中的新增功能。
ms.date: 12/18/2018
f1_keywords:
- VS.StartPage.WhatsNew
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 7307e180-ba28-4774-8a43-cbb980085a71
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 354d984ef8df7bd7c493a04eb0e27b439d82b0d1
ms.sourcegitcommit: 4f82de3fb0cfae226aef1abb40c47e63d2036a5c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72919148"
---
# <a name="whats-new-in-visual-studio-2017"></a>Visual Studio 2017 中的新增功能

针对[版本 15.9](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017) 而更新 

想从 Visual Studio 早期版本升级？ 以下是 Visual Studio 2017 的优势：为任何开发、应用和平台提供无与伦比的效率。 使用 Visual Studio 2017 开发适用于 Android、iOS、Windows、Linux、Web 和云的应用。 快速编码、轻松调试和诊断、时常测试，并且可以放心地进行发布。 还可通过构建自己的扩展，以便扩展和自定义 Visual Studio。 此版本发布之后，可使用版本控制、更具敏捷性且可高效协作！

>[!div class="button"]
>[下载 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

以下是我们自上一版本 Visual Studio 2015 以来所做更改的高级扼要重述：

* **[重新定义了基础知识](#redefined-fundamentals)** 。 新的安装体验意味着安装速度更快，并且能够在需要时立即安装。
* **[性能和工作效率](#performance-and-productivity)** 。 我们专注于新型、现代化的移动、云和桌面开发功能。 并且与以前相比，现在的 Visual Studio 启动速度更快、响应能力更强、使用的内存更少。
* **[使用 Azure 开发云应用](#cloud-app-development-with-azure)** 。 通过内置的 Azure 工具套件，可以轻松地创建由 Microsoft Azure 提供支持的云优先应用。 借助 Visual Studio，可以轻松配置、构建、调试、打包和部署 Azure 上的应用和服务。
* **[Windows 应用开发](#windows-app-development)** 。 使用 Visual Studio 2017 中的 UWP 模板创建一个可用于所有 Windows 10 设备的项目 &ndash; PC、平板电脑、电话、Xbox、HoloLens、 Surface Hub 等。
* **[移动应用开发](#mobile-app-development)** 。 使用 Xamarin 进行创新并快速得出结果。Xamarin 将多平台移动需求统一到一个核心基本代码和技能集。
* **[跨平台开发](#cross-platform-development)** 。 向任意目标平台无缝提供软件。 通过 Redgate 数据工具将 DevOps 流程扩展到 SQL Server 中，并在 Visual Studio 中安全地自动处理数据库部署。 或使用 .NET Core 编写在 Windows、Linux 和 macOS 操作系统上运行的未修改的应用和库。
* **[游戏开发](#games-development)** 。 借助 Visual Studio Tools Unity (VSTU)，可以使用 Visual Studio 在 C# 中编写游戏和编辑器脚本，随后使用其功能强大的调试器查找和修复错误。
* **[AI 开发](#ai-development)** 。 通过 Visual Studio Tools for AI，可使用 Visual Studio 的高效功能加快 AI 创新。 生成、测试和部署与 Azure 机器学习无缝集成的深入学习/AI 解决方案，从而实现强大的试验功能。

> [!NOTE]
> 有关 Visual Studio 2017 中新增功能的完整列表，请参阅[当前发行说明](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017)。 若要查看将来要推出的功能，请参阅[预览发行说明](/visualstudio/releasenotes/vs2017-preview-relnotes?context=visualstudio/default&contextView=vs-2017)。

以下是关于 Visual Studio 2017 中最值得关注的改进及新增功能的更多详细信息。

## <a name="redefined-fundamentals"></a>重新定义了基础知识

### <a name="a-new-setup-experience"></a>新的安装体验

通过 Visual Studio，可以在需要时更轻松快速地安装所需功能。 而且，还能完全卸载干净。

安装 Visual Studio 时，可以注意到最重要的更改是全新的安装体验。 在“工作负荷”  选项卡上，你将看到表示常见框架、语言和平台的分组安装选项。 它涵盖 Windows、Linux 和 iOS 上从 .NET 桌面开发到 C++ 应用程序开发的所有内容。

选择所需的工作负载，并在需要时对其进行更改。

![Visual Studio 2017 安装对话框](../install/media/install-visual-studio-enterprise.png)

并且还可以选择微调安装：

* 想要选择自己的组件而不是使用工作负载？ 请从安装程序选择“单个组件”选项卡  。
* 想要在不更改 Windows 语言选项的情况下立即安装语言包？ 选择安装程序的“语言包”  选项卡。
* **15.7 中的新增功能**：想要更改 Visual Studio 的安装位置？ 选择安装程序的“安装选项”  选项卡。

若要更深入地了解新的安装体验，包括指导你进行演练的分步说明，请参阅[安装 Visual Studio](../install/install-visual-studio.md) 页。

### <a name="a-focus-on-accessibility"></a>聚焦辅助功能

**15.3 中的新增功能**，我们进行了超过 1,700 处目标修补，以提高 Visual Studio 与许多客户使用的辅助技术的兼容性。 在十几种情况下，我们提高了与屏幕阅读器、高对比度主题和其他辅助技术的兼容性，比以往更兼容。 同时，我们还对调试程序、编辑器和 shell 进行了重大改进。

有关详细信息，请参阅博文 [Visual Studio 2017 版本 15.3 中的辅助功能改进](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)。

## <a name="performance-and-productivity"></a>性能和工作效率

### <a name="sign-in-across-multiple-accounts"></a>使用多个帐户登录

我们在 Visual Studio 中引入了新的标识服务，用户可在团队资源管理器、Azure 工具、Microsoft Store 发布等之间共享用户帐户。

你还能在更长的时间内保持登录状态。 Visual Studio 不会每隔 12 小时就要求你再次登录。 若要了解详细信息，请参阅 [Fewer Visual Studio Sign-in Prompts](https://devblogs.microsoft.com/visualstudio/fewer-visual-studio-sign-in-prompts/)（更少的 Visual Studio 登录提示）博客文章。

### <a name="start-visual-studio-faster"></a>更快地启动 Visual Studio

新的 Visual Studio 性能中心可以帮助你优化 IDE 启动速度。 性能中心列出了所有可能减缓 IDE 启动速度的扩展和工具窗口。 可用它来确定扩展何时启动，或工具窗口是否在启动时打开，从而提高启动性能。

### <a name="faster-on-demand-loading-of-extensions"></a>按需加载扩展速度更快

Visual Studio 可以移动自身的扩展（以及第三方扩展），从而根据需要加载扩展，而不是在 IDE 启动时加载。 想了解哪些扩展会影响启动、解决方案加载和键入性能？ 可以在“帮助” > “管理 Visual Studio 性能”中查看此信息   。

  ![Visual Studio 2017 中的“选项”对话框](media/vs2017ide-manage-vs-perf.png)

#### <a name="manage-your-extensions-with-roaming-extensions-manager"></a>利用漫游扩展管理器管理扩展

现在登录 Visual Studio 时，能更轻松地通过你最喜爱的扩展设置每个开发环境。 通过在云中创建同步列表，新漫游扩展管理器会跟踪所有你喜欢的扩展。

若要查看 Visual Studio 中的扩展列表，请单击“工具” > “扩展和更新”，再单击“漫游扩展管理器”    。

![Visual Studio 2017 -“扩展和更新”对话框](media/vs2017ide-extensions-and-updates.png)

漫游扩展管理器会跟踪安装的所有扩展，但你可以选择要添加到漫游列表的扩展。

![Visual Studio 2017 -“扩展和更新”对话框](media/vs2017ide-RoamingExtensionManager.png)

使用漫游扩展管理器时，列表中会出现 3 种图标类型：

* ![“漫游”图标](media/vs2017ide-roamedicon.png) **_漫游_** ：存在于漫游列表中，但未在计算机上安装的扩展。
  （可通过“下载”  按钮安装这些扩展。）
* ![“漫游且已安装”图标](media/vs2017ide-roamedinstalledicon.png) **_漫游且已安装_** ：存在于漫游列表中且已在此环境中安装的所有扩展。
  （如果确定不希望漫游，可通过“停止漫游”  按钮删除它们。）
* ![“已安装”图标](media/vs2017ide-installedicon.png) **_已安装_** ：此环境中已安装、但不属于漫游列表的所有扩展。
  （可通过“启动漫游”  按钮将扩展添加到漫游列表。）

在登录时下载的任何扩展将作为“漫游且已安装”  添加到列表中。 该扩展随即成为“漫游”列表的一部分，可以从任何计算机访问它。

### <a name="experience-live-unit-testing"></a>体验 Live Unit Testing

在 Visual Studio Enterprise 2017 中，当你进行编码时，实时单元测试能够在编辑器中提供实时单元测试结果和代码覆盖率。 该功能可用于 .NET Framework 及 .NET Core 的 C# 和 Visual Basic 项目，并支持 MSTest、xUnit 和 NUnit 三种测试框架。

![Live Unit Testing](media/lut-codewindow.png)

有关详细信息，请参阅 [Live Unit Testing 简介](../test/live-unit-testing-intro.md)。 有关 Visual Studio Enterprise 2017 各个版本的新增功能列表，请参阅 [ Live Unit Testing 中的新增功能](../test/live-unit-testing-whats-new.md)。

### <a name="set-up-a-cicd-pipeline"></a>设置 CI/CD 管道

#### <a name="automated-testing"></a>自动测试

自动测试是任何 DevOps 管道的重要组成部分。 用户可以在更短的周期内，持续且可靠地测试并发布解决方案。 CI/CD（持续集成和持续交付）流有助于改善进程效率。

有关自动测试的详细信息，请参阅博文 [DevOps 中用于自动测试的 CI/CD 管道](https://blogs.msdn.microsoft.com/visualstudioalmrangers/2017/04/20/set-up-a-cicd-pipeline-to-run-automated-tests-efficiently/)。

此外，若要详细了解[用于 Visual Studio 的持续交付工具](https://marketplace.visualstudio.com/items?itemName=VSIDEDevOpsMSFT.ContinuousDeliveryToolsforVisualStudio) DevLabs 扩展中的新增功能，请参阅博文[自信提交：提交时代码质量](https://devblogs.microsoft.com/visualstudio/committing-with-confidence-getting-code-quality-information-at-commit-time/)博客文章。

### <a name="visual-studio-ide-enhancements"></a>Visual Studio IDE 增强功能

#### <a name="multi-caret-editing"></a>多个插入点编辑

**15.8 中的新增功能**：现在很容易就能同时编辑文件中的多个位置。 首先在文件的多个位置创建插入点并选择内容。 然后，使用“多个插入点编辑”功能同时在两个或多个位置进行相同编辑。

有关详细信息，请参阅[查找和替换文本](finding-and-replacing-text.md)页面上的[多个插入点选择内容](finding-and-replacing-text.md#multi-caret-selection)部分。

#### <a name="keep-keybinding-profiles-consistent"></a>保证键绑定配置文件的一致性

**15.8 中的新增功能**：现可让不同工具中的键绑定与这两个新的键盘配置文件保持一致：Visual Studio Code 和 ReSharper (Visual Studio)。 可单击“工具” > “选项” > “常规” > “键盘”，在顶部下拉菜单下找到这些方案     。

  ![适用于 Visual Studio Code 和 ReSharper 的新的键绑定配置文件](media/vs-keyboard-mappings-code-resharper.png)

#### <a name="use-new-refactorings"></a>使用新的重构

重构是编写代码后对其进行改进的过程。 重构会更改代码的内部结构，而不更改其行为。 我们经常添加新的重构；下面仅是其中的一些：

* 添加参数（从 CallSite 添加）
* 生成重写函数
* 添加命名参数
* 为参数添加 null 检查
* 将数字分隔符插入文本
* 更改数字文本的基数（例如，从十六进制改为二进制）
* 转换 if-to-switch
* 删除未使用的变量

有关详细信息，请参阅[快速操作](common-quick-actions.md)。

#### <a name="interact-with-git"></a>与 Git 进行交互

在 Visual Studio 中处理项目时，可以对代码进行设置，并将代码快速提交和发布到 Git 服务。 还可以通过单击 IDE 右下角的按钮调出菜单来管理 Git 存储库。

![Visual Studio 2017 与 Git 进行交互的对话框](media/vsIDE-GitInteraction.png)

#### <a name="experience-improved-navigation-controls"></a>体验改进的导航控件

我们改善了导航体验，可让你更自信地从 A 导航到 B，同时减少此过程中的干扰。

* **15.4 中的新增功能**：转到定义（Ctrl+单击或 F12）&ndash; 鼠标用户按 Ctrl，然后单击成员，可以更轻松地导航到成员定义      。 通过按 **Ctrl** 并将鼠标悬停在代码符号上方，可在符号下方加下划线并将其转换为链接。 有关详细信息，请参阅[转到定义和查看定义](go-to-and-peek-definition.md)。

* **转到实现** (Ctrl+F12) &ndash; 从任何基类型或基成员转到各种实现   。

* **转到全部**（Ctrl+T 或 Ctrl+,）&ndash; 直接导航到任何文件/类型/成员/符号声明     。 可以筛选结果列表，也可以使用查询语法（例如使用“f searchTerm”导航到文件，使用“t searchTerm”导航到类型等）。

  ![改进后的“转到全部”](media/vs2017ide-navigation-go-to.png)

* **查找所有引用** (Shift+F12) &ndash; 通过语法着色，可以按项目、定义和路径的组合对“查找所有引用”的结果进行分组   。 还可以“锁定”结果，这样既可以继续查找其他引用，又不会丢失原始结果。

  ![新的“查找所有引用”工具](media/vs2017ide-find-all-references.png)

* **结构可视化工具** &ndash; 灰色的竖虚线（缩进参考线）可以在代码中起到关键点的作用，方便用户获得可视范围内的上下文。 可以通过热门的 Productivity Power Tool 进行识别。 使用该工具，无需滚动即可将代码可视化，并随时了解当前位于哪一代码块。 将鼠标悬停在行上时会显示工具提示，通过工具提示可以看到该代码块的开头及其父级。 通过 TextMate 语法以及 C#、Visual Basic 和 XAML 支持的所有语言都可以使用该工具。

  ![Visual Studio 2017 结构可视化工具](media/vsIDE-StructureVisualizer.png)

有关新的生产高效的功能的详细信息，请参阅 [Visual Studio 2017：工作效率、性能和合作伙伴](https://devblogs.microsoft.com/visualstudio/visual-studio-2017-productivity-performance-and-partners/)博客文章。

### <a name="visual-c"></a>Visual C++

Visual Studio 中的若干改进包括：使用 Visual Studio 分发 C++ 核心准则、通过添加对 C++11 和 C++ 功能的增强支持更新编译器以及添加和更新 C++ 库中的功能等。 我们还改进了 C++ IDE 的性能和安装工作负载等。

我们还修复了编译器和工具中的超过 250 个 bug 和已报告问题，其中很多是客户通过 [C++ 开发人员社区](https://developercommunity.visualstudio.com/spaces/62/index.html "C++ 开发人员社区")提交的。

有关完整的详细信息，请参阅 [Visual 2017 中 Visual C++ 的新增功能](/cpp/top/what-s-new-for-visual-cpp-in-visual-studio)页。

### <a name="debugging-and-diagnostics"></a>调试和诊断

#### <a name="run-to-click"></a>运行时单击

现在，在调试过程中快进变得更容易，无需在要停止的行上设置断点。 在调试器中停止时，单击出现在代码行旁边的图标即可。 下次在代码路径中命中该代码时，代码即会运行至该行并停在此处。

![Visual Studio 2017 调试 - 运行时单击](media/vs2017ide-RunToClick.png)

#### <a name="the-new-exception-helper"></a>新的异常帮助程序

新的异常帮助程序可以帮助你一目了然地查看异常信息。 异常信息以压缩形式呈现，你可以即时访问内部异常。 诊断 NullReferenceException 时，在异常帮助程序中可以快速查看为 null 的内容。

![Visual Studio 中“新异常帮助程序”对话框](media/vs2017ide-ExceptionHelper.png)

有关详细信息，请参阅 [Using the New Exception Helper in Visual Studio](https://devblogs.microsoft.com/devops/using-the-new-exception-helper-in-visual-studio-15-preview/)（使用 Visual Studio 中的新异常帮助器）博客文章。

#### <a name="snapshots-and-intellitrace-step-back"></a>快照和 IntelliTrace 后退

**15.5 中的新增功能**：IntelliTrace 后退会在每个断点处及调试器步骤事件发生时自动拍摄应用程序的快照。 凭借记录的快照便可以返回到上一个断点或步骤，并查看当时应用程序的状态。 如果希望查看以前的应用程序状态，但不想重新启动调试或重新创建所需应用状态，使用 IntelliTrace 后退可以节省时间。

可以通过使用“调试”工具栏中的“后退”和前进”按钮浏览和查看快照    。 这些按钮用于浏览“诊断工具”窗口中“事件”选项卡上显示的事件。   后退或前进到某个事件会自动激活所选事件的历史调试。

![Visual Studio 中“新异常帮助程序”对话框](../debugger/media/intellitrace-step-back-icons-description.png  "“后退”和“前进”按钮")

有关详细信息，请参阅[使用 IntelliTrace 后退查看快照](../debugger/view-historical-application-state.md)页。

### <a name="containerization"></a>容器化

容器可增加应用密度和降低部署成本，同时提高工作效率和 DevOps 灵活性。

#### <a name="docker-container-tooling"></a>Docker 容器工具

**15.5 中的新增功能**：

* Visual Studio 包含现在支持多阶段 Dockerfile 的用于 Docker 容器的工具，简化了创建优化容器映像的过程。
* 默认情况下，当打开具有 Docker 支持的项目时，Visual Studio 会在后台自动拉取、生成并运行必要的容器映像。 可以通过 Visual Studio 中的“在后台自动启动容器”设置禁用此操作  。

## <a name="cloud-app-development-with-azure"></a>使用 Azure 开发云应用

### <a name="azure-functions-tools"></a>Azure Functions 工具

作为“Azure 开发”工作负载的一部分，通过使用预编译的 C# 类库，我们加入了有助于开发 Azure 函数的工具。 现在，可以在自己的本地开发计算机上进行生成、运行和调试操作，并将其直接从 Visual Studio 发布至 Azure。

有关详细信息，请参阅[用于 Visual Studio 的 Azure Functions 工具](/azure/azure-functions/functions-develop-vs)页。

### <a name="debug-live-aspnet-apps-using-snappoints-and-logpoints-in-live-azure-applications"></a>在实时 Azure 应用程序中使用 snappoints 和 logpoints 调试实时 ASP.NET 应用

**15.5 中的新增功能**：当执行感兴趣的代码时，Snapshot Debugger 会为生产中的应用拍摄快照。 若要指示该调试器拍摄快照，可以在代码中设置快照点和记录点。 通过该调试器，可精确查看出错的内容，而不会影响生产应用程序的流量。 快照调试程序有助于大幅减少用于解决生产环境中发生的问题的时间。

快照集合适用于在 Azure App Service 中运行的以下 Web 应用：

* 在 .NET Framework 4.6.1 或更高版本上运行的 ASP.NET 应用程序。
* 在 Windows 中的 .Net Core 2.0 或更高版本上运行的 ASP.NET Core 应用程序。

有关详细信息，请参阅[使用 snappoints 和 logpoints 调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)

## <a name="windows-app-development"></a>Windows 应用程序开发

### <a name="universal-windows-platform"></a>通用 Windows 平台

通用 Windows 平台 (UWP) 是 Windows 10 的应用平台。 只需使用一个 API 集、一个应用包和一个存储便可开发适用于所有 Windows 10 设备的 UWP 应用 &ndash; PC、平板电脑、手机、Xbox、HoloLens、Surface Hub 等。 UWP 支持不同屏幕大小以及各种交互模型：无论是触控、鼠标及键盘、游戏控制器还是触笔。 UWP 应用的核心是这样一种理念，即用户可获得跨所有设备的移动体验，并可随时使用任何最便捷或最高效的设备完成手头任务。

![通用 Windows 平台](../cross-platform/media/uwp_coreextensions.png)

&mdash;从 C#、Visual Basic、C++ 或 JavaScript 中&mdash;选择首选的开发语言用来为 Windows 10 设备创建通用 Windows 平台应用。 Visual Studio 2017 提供所有语言的 UWP 应用模板，借助该模板可创建一个适用于所有设备的项目。 工作完成后，可以生成应用包，并从 Visual Studio 中将其提交到 Microsoft Store，以面向任何使用 Windows 10 设备的客户推出应用。

**15.5 中的新增功能**：Visual Studio 2017 版本 15.5 提供对 Windows 10 Fall Creators Update SDK (10.0.16299.0) 的最佳支持。 Windows 10 Fall Creators Update 也为 UWP 开发人员推出了许多改进内容。 以下是其中最重大的一些改进： 

* **支持 .NET Standard 2.0**<br/>除了简化的应用部署，Windows 10 Fall Creators Update 还是 Windows 10 第一个提供 .NET Standard 2.0 支持的版本。 实际上，[.NET Standard](https://devblogs.microsoft.com/dotnet/introducing-net-standard/) 是对任何 .NET 平台均可实现的基类库的引用实现。 .NET Standard 的设计目的是让 .NET 开发人员能够尽可能轻松地在其选择使用的任何 .NET 平台上共享代码。
* **最佳 UWP 和 Win32**<br/>已通过 [Desktop Bridge](/windows/uwp/porting/desktop-to-uwp-root) 改善 Windows 10 平台，以便 Windows 10 能为 .NET 开发人员提供更好的使用体验，无论他们当前关注的对象是 UWP、WPF、Windows Forms 还是 Xamarin。 使用 Visual Studio 2017 版本 15.5 中新的应用打包项目类型，可为 WPF 或 Windows 窗体项目创建 Windows 应用包，正如为 UWP 项目创建那样。 打包应用程序后，便获得所有 Windows 10 应用部署权益，并可选择通过 Microsoft Store（消费者应用）或商业版和教育版 Microsoft Store 进行分发。 由于打包的应用可在桌面上访问完整的 UWP API 界面和 Win32 API，因此现在可以使用 UWP API 和 Windows 10 功能逐渐实现 WPF 和 Windows 窗体应用程序的现代化。 此外，可将 Win32 组件包括在 UWP 应用程序中，凭借各种 Win32 功能，它们将在桌面上大放光彩。

有关 UWP 的详细信息，请参阅[开发用于通用 Windows 平台 (UWP) 的应用](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md)页。

## <a name="mobile-app-development"></a>移动应用开发

### <a name="xamarin"></a>Xamarin

作为“使用 .NET 的移动开发”工作负载的一部分，熟悉 C#、.NET 和 Visual Studio 的开发人员可使用 Xamarin 传递本地 Android、iOS 和 Windows 应用。 使用 Xamarin 开发移动应用（包括在 Android、iOS 和 Windows 设备上进行远程调试）时，开发人员同样可享受强大的功能和工作效率 &mdash; 无需学习 Objective-C 或 Java 等本机编程语言。

有关详细信息，请参阅 [Visual Studio 和 Xamarin](/xamarin/) 页。

### <a name="entitlements-editor"></a>权利编辑器

**15.3 中的新增功能**：为满足 iOS 开发需求，我们添加了独立的权利编辑器。 它包含便于浏览、用户友好的 UI。 要启动它，请双击 entitlements.plist  文件。

![Xamarin 的权利编辑器](media/xamarin-entitlements-editor.png)

### <a name="visual-studio-tools-for-xamarin"></a>Visual Studio Tools for Xamarin

**15.4 中的新增功能**：通过 Xamarin Live，开发人员可直接在 iOS 和 Android 设备上持续部署、测试和调试应用。 下载 Xamarin Live Player &mdash; 可在 App Store 或 Google Play 中获取 &mdash; 后，可将设备与 Visual Studio 配对，彻底改变生成移动应用的方式。 此功能现已包含在 Visual Studio 中，转到“工具” > “选项” > “Xamarin” > “其他” > “启用 Xamarin Live Player”即可启用此功能      。

![Xamarin Live Player 对、部署和实时编辑模式的动画](media/xamarinliveplayer.gif)

### <a name="support-for-google-android-emulator"></a>对 Google Android Emulator 的支持

**15.8 中的新增功能**：现在使用 Hyper-V 时，可将 Google Android Emulator 与其他基于 Hyper-V 的技术（例如 Hyper-V 虚拟机、Docker 工具和 HoloLens 模拟器等）并行使用。 （此功能需要 Windows 10 的 2018 年 4 月更新或更高版本。）

![基于 Hyper-V 技术的 Google Android Emulator](media/xamarin-hyperv-android-emulator.png)

#### <a name="xamarinandroid-designer-split-view-editor"></a>Xamarin.Android 设计器拆分视图编辑器

**15.8 中的其他新增功能**：显著改善了 Xamarin.Android 的设计器体验。 重点是新增的拆分视图编辑器，可用于同时创建、编辑和预览布局。

![Xamarin.Android 设计器拆分视图编辑器](media/android-designer-split-view.png)

有关详细信息，请参阅[硬件加速来提升模拟器性能](/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin)

### <a name="visual-studio-app-center"></a>Visual Studio 应用中心

**15.5 中的新增功能**：Visual Studio 应用中心（&mdash;已正式发布面向 Android、iOS、macOS 和 Windows 应用的版本&mdash;）提供用于管理应用生命周期的一切内容，包括自动生成、在云中对真实设备进行测试、面向 beta 测试人员和应用商店的分发以及通过故障和分析数据对实际使用情况进行监视。 所有功能都支持使用 Objective-C、Swift、Java、C#、Xamarin 和 React Native 编写的应用。

  ![Visual Studio 应用中心测试环境](media/app-center-test-env.png)

有关详细信息，请参阅[应用中心简介：在云中生成、测试、分发及监视应用](https://blogs.msdn.microsoft.com/vsappcenter/introducing-visual-studio-app-center/)博客文章。

## <a name="cross-platform-development"></a>跨平台开发

### <a name="redgate-data-tools"></a>Redgate 数据工具

现在可以在 Visual Studio 中使用 Redgate 数据工具，将 DevOps 功能扩展到 SQL Server 数据库开发。

Visual Studio 2017 Enterprise 随附：

* [Redgate ReadyRoll Core](https://www.red-gate.com/products/sql-development/sql-change-automation/?utm_source=microsoft&utm_medium=link&utm_campaign=readyroll&utm_term=docs-newinvs) 有助于开发迁移脚本、使用源代码管理功能来管理数据库更改，并安全地自动部署 SQL Server 数据库更改和应用更改。
* [Redgate SQL Prompt Core](https://www.red-gate.com/products/sql-development/sql-prompt/?utm_source=microsoft&utm_medium=link&utm_campaign=sqlprompt&utm_term=docs-newinvs) 提供智能代码填写帮助，有助于更快更准确地编写 SQL。 SQL Prompt 可自动完成数据库、系统对象和关键字，并在你键入时提供列建议。 这样一来，代码不仅更简洁，而且错误也更少，因为无需记住每个列名称或别名。

Visual Studio 2017 所有版本随附：

* [Redgate SQL Search](https://www.red-gate.com/products/sql-development/sql-search/?utm_source=microsoft&utm_medium=link&utm_campaign=sqlsearch&utm_term=docs-newinvs) 有助于跨多个数据库快速查找 SQL 片段和对象，从而提高工作效率。

若要了解详细信息，请参阅 [Visual Studio 2017 中的 Redgate Data Tools](https://devblogs.microsoft.com/visualstudio/redgate-data-tools-in-visual-studio-2017/) 博客文章。

### <a name="net-core"></a>.NET Core

.NET Core 是 .NET 标准的常规用途、模块化、跨平台和开放源代码实现，且包含许多与 .NET Framework 相同的 API。

.NET Core 平台由一些组件构成，其中包括托管的编译器、运行时、基类库和大量应用程序模型，如 ASP.NET Core。 .NET Core 支持三种主要的操作系统：Windows、Linux 和 macOS。 可以在设备、云和嵌入式/IoT 方案中使用 .NET Core。

当前，它还包括 Docker 支持。

**15.3 中的新增功能**：Visual Studio 2017 版本 15.3 支持 .NET Core 2.0 开发。 使用 .NET Core 2.0 前需分别下载并安装 .NET Core 2.0 SDK。

有关详细信息，请参阅 [.NET Core 指南](/dotnet/core/index)页。

## <a name="games-development"></a>游戏开发

### <a name="visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity

作为“适用于 Unity 的游戏开发”工作负载的一部分，我们添加了有助于跨平台开发的工具， 可用于创作 2D 和 3D 游戏及交互内容。 使用 Visual Studio 2017 和 Unity 5.6，一次创建即可发布到 21 个平台，包括所有移动平台、WebGL、Mac、PC 和 Linux 桌面、Web 或主机。

有关详细信息，请参阅 [Visual Studio Tools for Unity](../cross-platform/visual-studio-tools-for-unity.md) 页。

## <a name="ai-development"></a>AI 开发

### <a name="visual-studio-tools-for-ai"></a>Visual Studio Tools for AI

**15.5 中的新增功能**：立即使用 Visual Studio 的高效功能加快 AI 创新。 使用内置代码编辑器功能，如语法突出显示、IntelliSense 和文本自动格式设置。 可以通过对本地变量和模型使用单步调试，在本地环境中以交互方式测试深入学习应用程序。

  ![深入学习 IDE](../ai/media/about/ide.png)

有关详细信息，请参阅 [Visual Studio Tools for AI](../ai/about-ai-tools.md) 页。

## <a name="whats-next"></a>后续步骤

我们经常更新 Visual Studio 2017 的新功能，以使开发体验越来越好。 下面是一些最值得注意的更新（处于实验预览状态）的扼要重述：

* [实时共享](https://visualstudio.microsoft.com/services/live-share/)，一款新工具，可让你与团队成员共享代码库及其上下文，并直接从 Visual Studio 内获得即时双向协作  。 利用“实时共享”，团队成员可以无缝且安全地读取、导航、编辑和调试已与他们共享的项目。<br><br>有关详细信息，请参阅[实时共享常见问题解答](/visualstudio/liveshare/faq)。<br><br>
* **[IntelliCode](https://visualstudio.microsoft.com/services/intellicode/)** ，一种使用 AI 来增强软件开发的新功能，可提供更好的上下文感知代码、指导开发人员对其团队的模式和样式进行编码、找出难以捕捉的代码问题并将代码评审重点放在真正具有影响的方面。 <br><br>有关详细信息，请参阅 [IntelliCode 常见问题解答](/visualstudio/intellicode/faq)。

想要了解更多关于 Visual Studio 2017 的其他功能吗？ 请参阅 [Visual Studio 路线图](/visualstudio/productinfo/vs2018-roadmap)页。

请注意查看最新版本 [Visual Studio 2019](whats-new-visual-studio-2019.md)。

## <a name="contact-us"></a>联系我们

为什么将反馈发送至 Visual Studio 团队？ 因为我们严肃对待客户反馈。 这会给予我们巨大的行事动力。

如果有关于如何改进 Visual Studio 的建议，或想要详细了解产品支持选项，请参阅[向我们发送反馈](feedback-options.md)页。

### <a name="report-a-problem"></a>报告问题

有时，一条消息不足以说明所遇问题的总体影响。 如果遇到挂起、崩溃或其他性能问题，可利用“报告问题”  工具与我们轻松共享重现步骤和支持文件（如屏幕截图以及跟踪和堆转储文件）。 有关如何使用此工具的详细信息，请参阅[如何报告问题](how-to-report-a-problem-with-visual-studio.md)页。

## <a name="see-also"></a>请参阅

* [Visual Studio 2017 发行说明](/visualstudio/releasenotes/vs2017-relnotes)
* [Visual Studio 2017 SDK 的新增功能](/visualstudio/extensibility/what-s-new-in-the-visual-studio-2017-sdk)
* [Visual C++ 中的新增功能](/cpp/top/what-s-new-for-visual-cpp-in-visual-studio)
* [C# 中的新增功能](/dotnet/csharp/whats-new)
* [Team Foundation Server 中的新增功能](/tfs/server/whats-new?view=vsts)
* [Visual Studio for Mac 中的新增功能](https://visualstudio.microsoft.com/vs/visual-studio-mac/)
* [Visual Studio 2019 中的新增功能](whats-new-visual-studio-2019.md)
