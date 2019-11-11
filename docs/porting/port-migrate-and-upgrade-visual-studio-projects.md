---
title: 移植、迁移和升级项目
description: Visual Studio 的当前版本和早期版本中创建的项目的支持的参考。
ms.date: 10/17/2019
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload: multiple
f1_keywords:
- Win8ExpressDesktopBlock
- w8trefactor
- VS.ReviewProjectAndSolutionChangesDialog.UpgradeRetarget
- ProjectCompatibilityDlgHelpTopic
- VS.ReviewProjectAndSolutionChangesDialog.Upgrade
helpviewer_keywords:
- conversion, projects
- asset compatibility
- projects, conversion
ms.openlocfilehash: 9bc0436eac0460071d2393f8ff43178d49e8f7de
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72912008"
---
# <a name="project-migration-and-upgrade-reference-for-visual-studio"></a>Visual Studio 的项目迁移和升级参考

::: moniker range="vs-2017"

Visual Studio 的每个版本通常都支持大部分以前的项目、文件和其他资产类型。 可以[照常](../ide/solutions-and-projects-in-visual-studio.md)使用这些类型。如果不依赖新功能，Visual Studio 会尝试保留与旧版本（如 Visual Studio 2015、Visual Studio 2013 和 Visual Studio 2012）的向后兼容性。 （若要了解哪些功能特定于哪个版本，请参阅[发行说明](/visualstudio/releasenotes/vs2017-relnotes/)。）

对某些项目类型的支持也会随着时间的推移而更改。 较新版本的 Visual Studio 可能不再支持某些项目，或者需要更新项目，使其不再向后兼容。 有关迁移问题的当前状态，请参阅 [Visual Studio 开发人员社区站点](https://developercommunity.visualstudio.com)。

本文仅详细介绍 Visual Studio 2017 可迁移的项目类型。 本文不包括 Visual Studio 2017 中不再支持且因此无法迁移的项目类型。 本文也不包括没有迁移问题的受支持项目类型；此列表位于[平台目标以及兼容性](/visualstudio/productinfo/vs2017-compatibility-vs)中。

> [!IMPORTANT]
> 某些项目类型需要通过 Visual Studio 安装程序安装相应的工作负荷。 如果尚未安装工作负荷，Visual Studio 将报告未知的或不兼容的项目类型。 在这种情况下，请检查安装选项，然后重试。 同样，有关 Visual Studio 2017 中项目支持的详细信息，请参阅[平台目标以及兼容性](/visualstudio/productinfo/vs2017-compatibility-vs)。

## <a name="project-types"></a>项目类型

以下列表描述了 Visual Studio 2017 中对在之前版本中创建的项目的支持。

如果未看到本应在此列出的项目或文件类型，请查阅[本文的 Visual Studio 2015 版本](/visualstudio/porting/porting-migrating-and-upgrading-visual-studio-projects?view=vs-2015)，并使用此页底部的“发送以下项的反馈” > “本页”按钮来提供有关项目的详细信息   。 （如果使用匿名“此页是否有帮助？” 控件，则我们无法对你的反馈作出响应。）

| 项目类型 | 支持 |
| --- | --- |
| .NET Core 项目 (xproj) | 使用 Visual Studio 2015 旧预览工具创建的项目，其中包括 xproj 项目文件。 在 Visual Studio 2017 中，不支持 xproj 格式，除非迁移到 csproj 格式。 当你打开 xproj 文件时，系统将提示你将文件迁移到 SDK 样式的 .csproj 格式。 （创建 xproj 文件的备份。）Visual Studio 2015 及更早版本不支持使用 SDK 样式的 .csproj 项目。 有关详细信息，请参阅[将 .NET Core 项目迁移到 csproj 格式](/dotnet/core/migration/#visual-studio)。|
| ASP.NET Web 应用程序和启用了 Application Insights 的 ASP.NET Core Web 应用程序 | 对于每个 Visual Studio 用户，资源信息存储在每个用户实例的注册表中。 用户在不打开项目，但想要搜索 Azure Application Insights 数据的情况下，可使用此信息。 Visual Studio 2015 使用与 Visual Studio 2017 不同的注册表位置，且未发生冲突。<br/><br/>用户创建 ASP.NET Web 应用程序或 ASP.NET Core Web 应用程序后，资源存储在 .suo 文件中。 用户可在 Visual Studio 2015 或 2017 中打开项目，只要 Visual Studio 支持这两个版本中使用的项目和解决方案，资源信息就可用于这两个版本。 用户需要在每个产品上进行一次身份验证。 例如，如果使用 Visual Studio 2015 创建项目，然后在 Visual Studio 2017 中打开，则用户需要在 Visual Studio 2017 上进行身份验证。 |
| C#/Visual Basic Web 窗体或 Windows 窗体 | 可以在 Visual Studio 2017 和 Visual Studio 2015 中打开项目。 |
| 数据库单元测试项目（csproj、.vbproj） | 较旧的数据单元测试项目在 Visual Studio 2017 中加载，但将使用 GAC 版本的依赖关系。 若要升级单元测试项目以使用最新的依赖关系，请在“解决方案资源管理器”中右键单击该项目，然后选择“转换为 SQL Server 单元测试项目...”  。 |
| F# | Visual Studio 2017 可以打开 Visual Studio 2013 和 2015 中创建的项目。 但是，若要在这些项目中启用 Visual Studio 2017 功能，请打开项目属性，将目标 fsharp.core 更改为 F# 4.1。 此外，还需注意，.NET 工作负载不会默认选择 Visual Studio 安装程序中的“F# 语言支持”  选项；必须为工作负载选择该选项，或从“开发活动”  下的“个人组件”  选项卡中选择该选项。 |
| InstallShield<br/>MSI 安装程序 | 借助 [Visual Studio 安装程序项目扩展](https://marketplace.visualstudio.com/items?itemName=UnniRavindranathan-MSFT.MicrosoftVisualStudio2013InstallerProjects)，在 Visual Studio 2010 中创建的安装程序项目可在更高版本中打开。 另请参阅 [WiX Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)（WiX 工具集 Visual Studio 2017 扩展）。 Visual Studio 不再附带 InstallShield Limited Edition。 有关 Visual Studio 2017 的可用性，请咨询 [Flexera 软件](https://info.flexerasoftware.com/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio)。 |
| LightSwitch | Visual Studio 2017 中不再支持 LightSwitch。 使用 Visual Studio 2012 及早期版本创建并在 Visual Studio 2013 或 Visual Studio 2015 中打开的项目进行升级，之后只能在 Visual Studio 2013 或 Visual Studio 2015 中打开。 |
| Microsoft Azure Tools for Visual Studio | 若要打开这些类型的项目，请首先安装 [Azure SDK for .NET](https://azure.microsoft.com/downloads/)，然后打开该项目。 如有必要，请更新项目。 |
| 模型-视图-控制器框架 (ASP.NET MVC) | 对 MVC 版本和 Visual Studio 的支持：<ul><li>Visual Studio 2010 SP1 支持 MVC 2 和 MVC 3；通过[ASP.NET 4 MVC 4 for Visual Studio 2010 SP1 下载](https://www.microsoft.com/download/details.aspx?id=30683)添加 MVC 4 支持</li><li>Visual Studio 2012 仅支持 MVC 3 和 MVC 4</li><li>Visual Studio 2013 仅支持 MVC 4 和 MVC 5</li><li>Visual Studio 2017 和 Visual Studio 2015 支持 MVC 4（可打开现有项目但无法创建新项目）和 MVC 5</li></ul><br/>升级 MVC 版本：<ul><li>有关如何从 MVC 2 自动升级到 MVC 3 的信息，请参阅 [ASP.NET MVC 3 应用程序升级程序](https://archive.codeplex.com/?p=aspnet)。</li><li>有关如何从 MVC 2 手动升级到 MVC 3 的信息，请参阅 [将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 Tools 更新](https://archive.codeplex.com/?p=aspnet)。</li><li>有关如何从 MVC3 手动升级到 MVC 4 的信息，请参阅 [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](/aspnet/whitepapers/mvc4-release-notes)。 如果你的项目以 .NET Framework 3.5 SP1 为目标，则必须重定目标才能使用 .NET Framework 4。</li><li>有关如何从 MVC 4 手动升级到 MVC 5 的信息，请参阅[如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2](https://www.asp.net/mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2)。</li></ul> |
| 建模 | 如果允许 Visual Studio 自动更新项目，则可以在 Visual Studio 2015、Visual Studio 2013 或 Visual Studio 2012 中打开该项目。<br/><br/>Visual Studio 2015 和 Visual Studio 2017 之间未更改建模项目的格式，并且项目可以在任一版本中打开和修改。 但是，Visual Studio 2017 中的行为具有差异：<ul><li>建模项目现被称为菜单和模板中的“依赖关系验证”项目。</li><li>Visual Studio 2017 中不再支持 UML 关系图。 UML 文件照常在解决方案资源管理器中列出，但会以 XML 文件形式打开。 使用 Visual Studio 2015 查看、创建或编辑 UML 关系图。</li><li>在 Visual Studio 2017 中，生成建模项目时不再验证体系结构依赖关系。 但将在生成每个代码时进行验证。 此更改不会影响建模项目，但它需要对所验证的代码项目进行更改。 Visual Studio 2017 可以自动对代码项目执行必要的更改（[详细信息](/visualstudio/modeling/validate-code-with-layer-diagrams?view=vs-2017#live-dependency-validation)）。</li></ul> |
| MSI 安装程序 (vdproj) | 请参阅 InstallShield 项目。 |
| Office 2007 VSTO | 需要 Visual Studio 2017 单向升级。 |
| Office 2010 VSTO | 如果项目面向 .NET Framework 4，则可以在 Visual Studio 2010 SP1 及更高版本中打开此项目。 所有其他项目需要单向升级。 |
| Service Fabric (sfproj) | 可在 Visual Studio 2015 或 Visual Studio 2017 中打开 Service Fabric 应用程序项目，除非 Service Fabric 应用程序项目引用 ASP.NET Core 服务项目。 来自 Visual Studio 2015 在 Visual Studio 2017 中打开的 Service Fabric 项目从 xproj 格式单向迁移到 csproj。 请参阅此表前面的“.NET Core 项目 (xproj)”。 |
| SharePoint 2010 | 使用 Visual Studio 2017 打开 SharePoint 解决方案项目时，它将升级到 SharePoint 2013 或 SharePoint 2016。 “.NET 桌面开发”工作负载必须安装于 Visual Studio 2017 中，以便升级。<br/><br/>若要深入了解如何升级 SharePoint 项目，请参阅 [Upgrade to SharePoint 2013](https://technet.microsoft.com/library/cc303420.aspx)（升级到 SharePoint 2013）、[Update Workflow in SharePoint Server 2013](https://technet.microsoft.com/library/dn133867.aspx)（更新 SharePoint 2013 中的工作流）和 [Create the SharePoint Server 2016 farm for a database attach upgrade](https://technet.microsoft.com/library/cc263026(v=office.16).aspx)（创建 SharePoint Server 2016 场用于数据库附加升级）。 |
| SharePoint 2016 | 不能在 Visual Studio 2017 中打开 Office 开发人员工具预览版 2 中创建的 SharePoint 外接程序项目。 若要解除此限制，需要在 csproj vbproj 文件中将 `MinimumVisualStudioVersion` 更新到 12.0 并将 `MinimumOfficeToolsVersion` 更新到 12.2。 |
| Silverlight | Visual Studio 2017 不支持 Silverlight 项目。 若要继续使用 Silverlight 应用程序，请继续使用 Visual Studio 2015。 |
| SQL Server Reporting Services 和 SQL Server Analysis Services（SSRS、SSDT、SSAS、MSAS） | 通过 Visual Studio 库中的两个扩展提供对这些项目类型的支持：[Microsoft Analysis Services 建模项目](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)和 [Microsoft Reporting Services 项目](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)。 Visual Studio 2017 的数据存储和处理工作负载中还包括 SSDT 支持。 有关详细信息，请参阅[下载并安装 SQL Server Data Tools (SSDT) for Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt) 页。|
| SQL Server Integration Services (SSIS) | 可通过 SQL Server Data Tools (SSDT) 获取 Visual Studio 2017 支持。 有关详细信息，请参阅[下载并安装 SQL Server Data Tools (SSDT) for Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt) 页和 [SQL Server Integration Services (SSIS)](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/bg-p/SSIS) 团队博客。 |
| Visual C++ | Visual Studio 2017 可用于在 Visual Studio 的早期版本中（追溯到 Visual Studio 2010 ）创建的项目中工作。 首次打开项目时，可以选择升级到最新的编译器和工具集，或者继续使用原始编译器和工具集。 如果选择继续使用原始编译器和工具集，Visual Studio 2017 将不会修改项目文件，并使用早期版本 Visual Studio 安装中的工具集来生成项目。 选择继续使用原始编译器和工具集意味着你仍可以在 Visual Studio 的原始版本中打开项目（如有必要）。 有关详细信息，请参阅 [使用 Visual Studio 中的本机多重目标生成旧项目](/cpp/porting/use-native-multi-targeting)。 |
| Visual Studio 扩展性/VSIX | 更新 MinimumVersion 14.0 或更低版本中的项目以声明 MinimumVersion 15.0，这样可防止在早期版本的 Visual Studio 中打开该项目。 若要允许在早期版本中打开项目，请将 MinimumVersion 设置为 `$(VisualStudioVersion)`。 另请参阅[如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。 |
| Visual Studio 实验室管理工具版 | 你可以使用 Microsoft 测试管理器或 Visual Studio 2010 SP1 及更高版本打开在以上任一版本中创建的环境。 但对于 Visual Studio 2010 SP1，在可以创建环境之前，Microsoft 测试管理器的版本必须与 Team Foundation Server 的版本匹配。 |
| Visual Studio Tools for Apache Cordova | 可以在 Visual Studio 2017 中打开项目，但此项目不具有向后兼容性。 从 Visual Studio 2015 中打开某个项目时，系统将提示允许修改项目。 此修改会将项目升级为使用工具集而非 `taco.json` 文件来管理 Cordova 库、该库的平台、插件和节点/npm 依赖关系的版本控制。 有关详细信息，请参阅[迁移指南](/visualstudio/cross-platform/tools-for-cordova/first-steps/migrate-from-visual-studio-2015)。 |
| Web 部署 (wdproj) | Visual Studio 2012 中已删除对 Web 部署项目的支持，而添加了发布配置文件支持。 在 Visual Studio 2017 中没有相应的功能，因此，此类项目没有自动迁移路径。 而是，在文本编辑器中打开 wdproj 文件，并将任何自定义项复制粘贴到 pubxml（发布配置文件）文件中，如 [StackOverflow](https://stackoverflow.com/a/12061065/1203388) 中所述。 |
| Windows Communication Foundation, Windows Workflow Foundation | 可以在 Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 和 Visual Studio 2012 中打开此项目 |
| Windows Presentation Foundation | 可以在 Visual Studio 2017、Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。 |
| Windows 应用商店/手机应用 | Visual Studio 2017 不支持 Windows Store 8.1 和 8.0 的项目，也不支持 Windows Phone 8.1 和 8.0 的项目。 若要继续使用这些应用，请继续使用 Visual Studio 2015。 要继续使用 Windows Phone 7.x 项目，请使用 Visual Studio 2012。 |

## <a name="how-visual-studio-decides-when-to-migrate-a-project"></a>Visual Studio 如何决定迁移项目的时间

每个新版本的 Visual Studio 通常都会尝试与之前的版本保持兼容，以便在不同版本中打开、修改和构建同一项目。 但是，随着时间的推移，会出现不可避免的更改，使某些项目类型不再受支持。 （请参阅[平台目标以及兼容性](/visualstudio/productinfo/vs2017-compatibility-vs)，了解 Visual Studio 2017 支持的项目类型。）在这些情况下，较新版本的 Visual Studio 不会加载该项目并且不提供迁移路径；需要在支持该项目的 Visual Studio 早期版本中维护该项目。

在其他情况下，较新版本的 Visual Studio 可以打开项目，但必须以可能导致其与之前的版本不兼容的方式更新或迁移该项目。 Visual Studio 使用大量条件来确定是否需要此类迁移：

- 与平台目标版本（Visual Studio 2013 RTM 及更高版本）的兼容性。

- 设计时资产与 Visual Studio 早期版本的兼容性。 （即，Visual Studio 2017、Visual Studio 2015 RTM & Update 3、Visual Studio 2013 RTM & Update 5、Visual Studio 2012 Update 4、Visual Studio 2010 SP 1 的不同通道。）Visual Studio 2017 旨在正常退出已弃用的设计时资产，而不损坏这些资产，使之前的版本仍可以打开该项目。

- 新设计时资产是否会破坏与早期版本（Visual Studio 2013 RTM & Update 5 及更高版本）的兼容性。

相关项目类型的工程所有者可查看这些条件，并确定需要支持、兼容性和迁移的位置。 同样，如果可能，Visual Studio 尝试保持 Visual Studio 各版本之间的透明兼容性，这意味着在某一 Visual Studio 版本中创建和修改的项目也可在其他版本中工作。

但是，如果与本文中所述的某些项目类型一样，不可能有此兼容性，那么 Visual Studio 会打开升级向导进行必要的单向更改。

此类单向更改可能涉及更改项目文件中的 `ToolsVersion` 属性，该属性明确表示哪个 MSBuild 版本可以将项目的源代码转变为最终所需的可运行且可部署的项目。 也就是说，导致项目与 Visual Studio 早期版本不兼容的不是 Visual Studio 版本，而是由 `ToolsVersion` 确定的 MSBuild 版本   。 只要 Visual Studio 版本包含与项目中的 `ToolsVersion` 匹配的 MSBuild 工具链，Visual Studio 就可以调用该工具链来生成项目。

为了最大限度保持与较旧版本中创建的项目的兼容性，Visual Studio 2017 包含了必要的 MSBuild 工具链来支持 `ToolsVersion` 15、14、12 和 4。 使用任意这些 `ToolsVersion` 值的项目都可进行成功的生成。 （再次强调，有关 Visual Studio 2017 是否支持项目类型的主题，请参阅[平台目标以及兼容性](/visualstudio/productinfo/vs2017-compatibility-vs)。）

在此上下文中，会自然而然出现一个问题：是否应该尝试将项目手动更新或迁移到新的 `ToolsVersion` 值。 没有必要做出该更改，进行该更改可能会产生许多错误和警告，需要修复它们并再次生成项目。 此外，如果 Visual Studio 以后不支持特定的 `ToolsVersion`，那么打开项目会触发项目迁移过程，这是因为必须更改 `ToolsVersion` 值。 在这种情况下，该特定项目类型的子系统确切地知道要更改的内容，并且可以按前文所述自动完成更改。

## <a name="next-steps"></a>后续步骤

如需进一步讨论，请参阅以下文章：

- [ToolsVersion 指南](../msbuild/msbuild-toolset-toolsversion.md)
- [Framework 目标指南](../ide/visual-studio-multi-targeting-overview.md)

## <a name="see-also"></a>请参阅

[Visual Studio 2019 的项目迁移和升级参考](port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2019)

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 的每个版本通常都支持大部分以前的项目、文件和其他资产类型。 可以[照常](../ide/solutions-and-projects-in-visual-studio.md)使用这些类型。如果不依赖新功能，Visual Studio 会尝试保留与旧版本（如 Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 和 Visual Studio 2012）的向后兼容性。 （若要了解哪些功能特定于哪个版本，请参阅[发行说明](/visualstudio/releases/2019/release-notes/)。）

对某些项目类型的支持会随着时间的推移而更改。 较新版本的 Visual Studio 可能不再支持某些项目，或者可能需要更新项目，使其不再向后兼容。 有关迁移问题的当前状态，请参阅 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com)。

本文详细介绍 Visual Studio 2019 可迁移的项目类型。 它还包括 Visual Studio 2019 弃用的或者即将弃用的项目类型的信息。 本文不包括 Visual Studio 2019 中不再支持且因此无法迁移的项目类型。 本文也不包括没有迁移问题的受支持项目类型；此列表位于[平台目标以及兼容性](/visualstudio/releases/2019/compatibility)中。

> [!IMPORTANT]
> 某些项目类型需要通过 Visual Studio 安装程序安装特定的工作负荷。 如果尚未安装工作负荷，Visual Studio 将报告未知的或不兼容的项目类型。 在这种情况下，请检查安装选项，然后重试。 有关 Visual Studio 2019 中项目支持的详细信息，请参阅[平台目标以及兼容性](/visualstudio/releases/2019/compatibility)。

## <a name="project-types"></a>项目类型

以下列表描述了 Visual Studio 2019 中对在之前版本中创建的项目的支持。

如果在此处未看到任何项目或文件类型（此处本应出现这些内容），请参阅[本文的 Visual Studio 2017 版本](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects?view=vs-2017)。 还可以使用本页底部的“发送有关以下内容的反馈”   > “本页”  按钮来提供项目的详细信息。 （如果使用匿名“此页是否有帮助？” 控件，则我们无法对你的反馈作出响应。）

| 项目类型 | 支持 |
| --- | --- |
| .NET Core 项目 (xproj) | 使用 Visual Studio 2015 旧预览工具创建的项目，其中包括 xproj 项目文件。<br/><br/>Visual Studio 2017：不支持 xproj 格式，除非迁移到 csproj 格式。 当你打开 xproj 文件时，系统将提示你将文件迁移到 SDK 样式的 .csproj 格式。 （创建 xproj 文件的备份。）Visual Studio 2015 及更早版本不支持使用 SDK 样式的 .csproj 项目。 <br/><br/>Visual Studio 2019：在版本 16.3 和更高版本中，无法加载或迁移 xproj 项目。 有关详细信息，请参阅[将 .NET Core 项目迁移到 csproj 格式](/dotnet/core/migration/#visual-studio)。|
| ASP.NET Web 应用程序和启用了 Application Insights 的 ASP.NET Core Web 应用程序 | 对于每个 Visual Studio 用户，资源信息存储在每个用户实例的注册表中。 用户在不打开项目，但想要搜索 Azure Application Insights 数据的情况下，可使用此信息。 Visual Studio 2015 使用与 Visual Studio 2017 和 Visual Studio 2019 不同的注册表位置，且未发生冲突。<br/><br/>用户创建 ASP.NET Web 应用程序或 ASP.NET Core Web 应用程序后，资源存储在 .suo 文件中。 用户可在 Visual Studio 2015、Visual Studio 2017 或者 Visual Studio 2019 中打开项目，只要 Visual Studio 支持每个版本中使用的项目和解决方案，资源信息就可用于这些版本。 用户需要在每个产品上进行一次身份验证。 例如，如果使用 Visual Studio 2017 创建项目，然后在 Visual Studio 2019 中打开，则用户需要在 Visual Studio 2019 上进行身份验证。 |
| C#/Visual Basic Web 窗体或 Windows 窗体 | 可以在 Visual Studio 2019、Visual Studio 2017 和 Visual Studio 2015 中打开项目。 |
| 编码的 UI 测试 | 在 Visual Studio 2019 中，已弃用自动 UI 驱动功能测试的编码的 UI 测试。 <br/><br/>Visual Studio 2019 将是编码的 UI 测试的最后一个版本。 建议使用 Selenium 来测试 Web 应用，使用 Appium 和 WinAppDriver 来测试桌面和 UWP 应用。 |
| 数据库单元测试项目（csproj、.vbproj） | 较旧的数据单元测试项目在 Visual Studio 2019 中加载，但将使用 GAC 版本的依赖关系。 若要升级单元测试项目以使用最新的依赖关系，请在“解决方案资源管理器”中右键单击该项目，然后选择“转换为 SQL Server 单元测试项目...”  。 |
| F# | Visual Studio 2019 可以打开 Visual Studio 2013、Visual Studio 2015 和 Visual Studio 2017 中创建的项目。 对于新项目来说，与较旧的 Visual Studio 模板的关键区别是 FSharp.Core 版本现在始终是 NuGet 包。 默认情况下，F# 随任何 .NET 工作负载安装。|
| InstallShield<br/>MSI 安装程序 | 借助 [Visual Studio 安装程序项目扩展](https://marketplace.visualstudio.com/items?itemName=UnniRavindranathan-MSFT.MicrosoftVisualStudio2013InstallerProjects)，在 Visual Studio 2010 中创建的安装程序项目可在更高版本中打开。 另请参阅 [WiX Toolset Visual Studio 2017 Extension](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)（WiX 工具集 Visual Studio 2017 扩展）。 Visual Studio 不再附带 InstallShield Limited Edition。 有关 Visual Studio 2019 的可用性，请咨询 [Flexera 软件](https://info.flexerasoftware.com/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio)。 |
| LightSwitch | Visual Studio 2019 或 Visual Studio 2017 不再支持 LightSwitch。 使用 Visual Studio 2012 及早期版本创建并在 Visual Studio 2013 或 Visual Studio 2015 中打开的项目进行升级，之后只能在 Visual Studio 2013 或 Visual Studio 2015 中打开。 |
| 负载测试 | Visual Studio 2019 已弃用 Web 性能和负载测试功能。 <br/><br/>Visual Studio 2019 将是负载测试的最后一个版本。 使用替代的负载测试工具（例如 Apache JMeter、Akamai CloudTest、Blazemeter）。  |
| Microsoft Azure Tools for Visual Studio | 若要打开这些类型的项目，请首先安装 [Azure SDK for .NET](https://azure.microsoft.com/downloads/)，然后打开该项目。 如有必要，请更新项目。 |
| Microsoft 测试管理器 | 从 Visual Studio 2019 开始，Visual Studio 中将不再随附 Microsoft 测试管理器和 Feedback Client。 <br/><br/>利用 Azure Test Plans（Azure DevOps 的一部分）满足手动和探索性测试需求。 有关详细信息，请参阅 Azure DevOps 文档中的[有关 Microsoft 测试管理器使用情况的指南](/azure/devops/test/mtm/guidance-mtm-usage?view=azure-devops)页。 |
| 模型-视图-控制器框架 (ASP.NET MVC) | 对 MVC 版本和 Visual Studio 的支持：<ul><li>Visual Studio 2010 SP1 支持 MVC 2 和 MVC 3；通过[ASP.NET 4 MVC 4 for Visual Studio 2010 SP1 下载](https://www.microsoft.com/download/details.aspx?id=30683)添加 MVC 4 支持</li><li>Visual Studio 2012 仅支持 MVC 3 和 MVC 4</li><li>Visual Studio 2013 仅支持 MVC 4 和 MVC 5</li><li>Visual Studio 2019、Visual Studio 2017 和 Visual Studio 2015 支持 MVC 4（可打开现有项目但无法创建新项目）和 MVC 5</li></ul><br/>升级 MVC 版本：<ul><li>有关如何从 MVC 2 自动升级到 MVC 3 的信息，请参阅 [ASP.NET MVC 3 应用程序升级程序](https://archive.codeplex.com/?p=aspnet)。</li><li>有关如何从 MVC 2 手动升级到 MVC 3 的信息，请参阅 [将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 Tools 更新](https://archive.codeplex.com/?p=aspnet)。</li><li>有关如何从 MVC3 手动升级到 MVC 4 的信息，请参阅 [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](/aspnet/whitepapers/mvc4-release-notes)。 如果你的项目以 .NET Framework 3.5 SP1 为目标，则必须重定目标才能使用 .NET Framework 4。</li><li>有关如何从 MVC 4 手动升级到 MVC 5 的信息，请参阅[如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2](https://www.asp.net/mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2)。</li></ul> |
| 建模 | 如果允许 Visual Studio 自动更新项目，则可以在 Visual Studio 2015、Visual Studio 2013 或 Visual Studio 2012 中打开该项目。<br/><br/>自 Visual Studio 2015 以来，建模项目格式没有发生变化，可以在这些版本中打开和修改项目。 但是，Visual Studio 2017 和 Visual Studio 2019 中的行为具有差异：<ul><li>建模项目现被称为菜单和模板中的“依赖关系验证”项目。</li><li>Visual Studio 2017 和 Visual Studio 2019 不再支持 UML 关系图。 UML 文件照常在解决方案资源管理器中列出，但会以 XML 文件形式打开。 使用 Visual Studio 2015 查看、创建或编辑 UML 关系图。</li><li>在 Visual Studio 2019 中，生成建模项目时不再验证体系结构依赖关系。 但将在生成每个代码时进行验证。 此更改不会影响建模项目，但它需要对所验证的代码项目进行更改。 Visual Studio 2019 可以自动对代码项目执行必要的更改。</li></ul> |
| MSI 安装程序 (vdproj) | 请参阅 InstallShield 项目。 |
| Office 2007 VSTO | 需要 Visual Studio 2019 单向升级。 |
| Office 2010 VSTO | 如果项目面向 .NET Framework 4，则可以在 Visual Studio 2010 SP1 及更高版本中打开此项目。 所有其他项目需要单向升级。 |
| 可移植类库 (PCL) | 当前不支持可移植类库（或 PCL）。 Visual Studio 2019 将仍然会打开并生成它们，但是不可能创建新的 PCL 项目。 建议将 PCL 项目中的代码迁移到 .NET Standard 项目。<br/><br/>默认情况下将不再包含 PCL 支持，但在 Visual Studio 的“单个组件”选项卡上可以使用。 |
| Python 工作负荷 | Visual Studio 2019 删除了 Python Windows IoT Core 应用的支持。 在 Visual Studio 2019 预览版中没有相应的功能，因此，此类项目没有自动迁移路径。<br/><br/>可以继续使用 Visual Studio 2017。 |
| R Tools for Visual Studio | 已从 Visual Studio 2019 的数据科学工作负载中删除了针对 Visual Studio 的 R 工具。<br/><br/>可以继续使用 Visual Studio 2017 或替代产品（例如 RStudio）。 |
| Service Fabric (sfproj) | 可在 Visual Studio 2015、Visual Studio 2017 或 Visual Studio 2019 预览版中打开 Service Fabric 应用程序项目，除非 Service Fabric 应用程序项目引用 ASP.NET Core 服务项目。 来自 Visual Studio 2015 在 Visual Studio 2017 或 Visual Studio 2019 预览版中打开的 Service Fabric 项目从 xproj 格式单向迁移到 csproj。 请参阅此表前面的“.NET Core 项目 (xproj)”。 |
| SharePoint 2010 | 使用 Visual Studio 2019 打开 SharePoint 解决方案项目时，它将升级为 SharePoint 2013 或 SharePoint 2016。 “.NET 桌面开发”工作负载必须安装到 Visual Studio 2019 中，以便升级。<br/><br/>若要深入了解如何升级 SharePoint 项目，请参阅 [Upgrade to SharePoint 2013](https://technet.microsoft.com/library/cc303420.aspx)（升级到 SharePoint 2013）、[Update Workflow in SharePoint Server 2013](https://technet.microsoft.com/library/dn133867.aspx)（更新 SharePoint 2013 中的工作流）和 [Create the SharePoint Server 2016 farm for a database attach upgrade](https://technet.microsoft.com/library/cc263026(v=office.16).aspx)（创建 SharePoint Server 2016 场用于数据库附加升级）。 |
| SharePoint 2016 | 不能在 Visual Studio 2019 中打开 Office 开发人员工具预览版 2 中创建的 SharePoint 加载项项目。 若要解除此限制，需要在 csproj vbproj 文件中将 `MinimumVisualStudioVersion` 更新到 12.0 并将 `MinimumOfficeToolsVersion` 更新到 12.2。 |
| Silverlight | Visual Studio 2019 不支持 Silverlight 项目。 若要继续使用 Silverlight 应用程序，请继续使用 Visual Studio 2015。 |
| SQL - Redgate | Visual Studio 安装程序中不再随附 Redgate 的 SQL Change Automation Core（以前称为 ReadyRoll Core）、SQL Prompt Core 和 SQL 搜索。<br/><br/>可以继续使用 Visual Studio 2017 获取这些功能。 在 Visual Studio 2019 中，可以升级到 Redgate 的 SQL Toolbelt 中提供的付费 SQL Change Automation 和 SQL Prompt 产品。|
| SQL Server Reporting Services 和 SQL Server Analysis Services（SSRS、SSDT、SSAS、MSAS） | 通过 Visual Studio 库中的两个扩展提供对这些项目类型的支持：[Microsoft Analysis Services 建模项目](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)和 [Microsoft Reporting Services 项目](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)。 Visual Studio 2019 的数据存储和处理工作负载中还包括 SSDT 支持。 有关详细信息，请参阅[下载并安装 SQL Server Data Tools (SSDT) for Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt) 页。 |
| SQL Server Integration Services (SSIS) | Visual Studio 2019 的支持现已推出。 有关详细信息，请参阅商城上的[下载并安装 SQL Server Data Tools (SSDT) for Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt) 页、[SQL Server Integration Services (SSIS)](https://techcommunity.microsoft.com/t5/SQL-Server-Integration-Services/bg-p/SSIS) 团队博客和 [SQL Server Integration Services 项目](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects&ssr=false#overview)页。 |
| 测试窗口扩展 | 在 Visual Studio 2019 中，删除了一些以前标记为公开但从未正式记录过的测试窗口 API。 在 Visual Studio 2017 中，广泛可见的 API 被标记为已弃用，以便为扩展维护人员提供早期警告。 据我们所知，很少有扩展依赖这些 API。 有关详细信息和更新，请查看[已弃用的与测试相关的 API 完整列表](https://github.com/Microsoft/vstest/issues/1830)。 如果这会影响你的方案，请在[开发人员社区](https://developercommunity.visualstudio.com)上告诉我们。 |
| Visual C++ | Visual Studio 2019 可用于在 Visual Studio 的早期版本中（追溯到 Visual Studio 2010）创建的项目中工作。 首次打开项目时，可以选择升级到最新的编译器和工具集，或者继续使用原始编译器和工具集。 如果选择继续使用原始编译器和工具集，Visual Studio 2019 将不会修改项目文件，并使用早期版本 Visual Studio 安装中的工具集来生成项目。 选择继续使用原始编译器和工具集意味着你仍可以在 Visual Studio 的原始版本中打开项目（如有必要）。 有关详细信息，请参阅 [使用 Visual Studio 中的本机多重目标生成旧项目](/cpp/porting/use-native-multi-targeting)。 |
| Visual Studio 扩展性/VSIX | 更新 MinimumVersion 14.0 或更低版本中的项目以声明 MinimumVersion 15.0，这样可防止在早期版本的 Visual Studio 中打开该项目。 若要允许在早期版本中打开项目，请将 MinimumVersion 设置为 `$(VisualStudioVersion)`。 另请参阅[如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。 |
| Visual Studio 实验室管理工具版 | 你可以使用 Microsoft 测试管理器或 Visual Studio 2010 SP1 及更高版本打开在以上任一版本中创建的环境。 但对于 Visual Studio 2010 SP1，在可以创建环境之前，Microsoft 测试管理器的版本必须与 Team Foundation Server 的版本匹配。 |
| Visual Studio Tools for Apache Cordova | 在 Visual Studio 2019 中删除了对 Apache Cordova 的支持。 在 Visual Studio 2019 中没有相应的功能，因此，此类项目没有自动迁移路径。<br/><br/>可以将 Cordova 工具用于 Visual Studio Code 扩展（其为最新版本的 Cordova 提供支持），也可以继续使用 Visual Studio 2017。 |
| Web 部署 (wdproj) | Visual Studio 2012 中已删除对 Web 部署项目的支持，而添加了发布配置文件支持。 在 Visual Studio 2019 中没有相应的功能，因此，此类项目没有自动迁移路径。 而是，在文本编辑器中打开 wdproj 文件，并将任何自定义项复制粘贴到 pubxml（发布配置文件）文件中，如 [StackOverflow](https://stackoverflow.com/a/12061065/1203388) 中所述。 |
| Windows Communication Foundation, Windows Workflow Foundation | 可以在 Visual Studio 2019、Visual Studio 2017、Visual Studio 2015、Visual Studio 2013 和 Visual Studio 2012 中打开此项目。 |
| Windows Presentation Foundation | 可以在 Visual Studio 2019、Visual Studio 2017、Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。 |
| Windows Phone 应用 | Visual Studio 2019 不支持 Windows Phone 项目。 <br/><br/>要继续使用 Windows Phone 8.x 应用，请使用 Visual Studio 2015。 要继续使用 Windows Phone 7.x 项目，请使用 Visual Studio 2012。 |
| Windows 应用商店应用程序 | Visual Studio 2019 不支持 JavaScript Universal Windows 项目。 要继续使用这些项目，请使用 Visual Studio 2017。 <br/><br/>Windows 10 Fall Creators Update（内部版本 16299）之前的 Windows 10 SDK 已从 Visual Studio 2019 安装程序中删除。 可以手动下载旧版 SDK，也可以重定向项目以使用较新的 SDK。<br/><br/>不支持使用 project.json 的通用 Windows 项目。 建议升级这些项目以使用包引用。 或者，在 project.json 文件中添加对 Microsoft.NET.Test.Sdk 版本 16.0.0.0 的引用。<br/><br/>Visual Studio 2019 不支持 Windows Store 8.1 和 8.0 的项目。 要继续使用这些应用，请继续使用 Visual Studio 2015。 |
| Xamarin | 已删除适用于 Visual Studio 和 Visual Studio for Mac 的 Xamarin Live Player 扩展。 这会删除配对屏幕和任何集成。 改用内置的 Xamarin.Forms 预览器。<br/><br/>适用于 Android 的 Visual Studio 仿真程序已从 Visual Studio 安装程序中删除。 改用 Google Android 仿真程序中的新的 Hyper-V 支持。 |

## <a name="how-visual-studio-decides-when-to-migrate-a-project"></a>Visual Studio 如何决定迁移项目的时间

每个新版本的 Visual Studio 通常都会尝试与之前的版本保持兼容，以便在不同版本中打开、修改和构建同一项目。 但是，随着时间的推移，会出现不可避免的更改，使某些项目类型不再受支持。 （请参阅[平台目标以及兼容性](/visualstudio/releases/2019/compatibility)，了解 Visual Studio 2019 支持的项目类型。）在这些情况下，较新版本的 Visual Studio 不会加载该项目并且不提供迁移路径；需要在支持该项目的 Visual Studio 早期版本中维护该项目。

在其他情况下，较新版本的 Visual Studio 可以打开项目，但必须以可能导致其与之前的版本不兼容的方式更新或迁移该项目。 Visual Studio 使用大量条件来确定是否需要此类迁移：

- 与平台目标版本（Visual Studio 2013 RTM 及更高版本）的兼容性。

- 设计时资产与 Visual Studio 早期版本的兼容性。 （即，Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 RTM & Update 3、Visual Studio 2013 RTM & Update 5、Visual Studio 2012 Update 4、Visual Studio 2010 SP 1 的不同通道。）Visual Studio 2019 旨在正常退出已弃用的设计时资产，而不损坏这些资产，使之前的版本仍可以打开该项目。

- 新设计时资产是否会破坏与早期版本（Visual Studio 2013 RTM & Update 5 及更高版本）的兼容性。

相关项目类型的工程所有者可查看这些条件，并确定需要支持、兼容性和迁移的位置。 同样，如果可能，Visual Studio 尝试保持 Visual Studio 各版本之间的透明兼容性，这意味着在某一 Visual Studio 版本中创建和修改的项目也可在其他版本中工作。

但是，如果与本文中所述的某些项目类型一样，不可能有此兼容性，那么 Visual Studio 会打开升级向导进行必要的单向更改。

此类单向更改可能涉及更改项目文件中的 `ToolsVersion` 属性，该属性明确表示哪个 MSBuild 版本可以将项目的源代码转变为最终所需的可运行且可部署的项目。 也就是说，导致项目与 Visual Studio 早期版本不兼容的不是 Visual Studio 版本，而是由 `ToolsVersion` 确定的 MSBuild 版本   。 只要 Visual Studio 版本包含与项目中的 `ToolsVersion` 匹配的 MSBuild 工具链，Visual Studio 就可以调用该工具链来生成项目。

为了最大限度保持与较旧版本中创建的项目的兼容性，Visual Studio 2019 包含了必要的 MSBuild 工具链来支持 `ToolsVersion` 15、14、12 和 4。 使用任意这些 `ToolsVersion` 值的项目都可进行成功的生成。 （再次强调，有关 Visual Studio 2019 是否支持项目类型的主题，请参阅[平台目标以及兼容性](/visualstudio/releases/2019/compatibility)。）

在此上下文中，会自然而然出现一个问题：是否应该尝试将项目手动更新或迁移到新的 `ToolsVersion` 值。 没有必要做出该更改，进行该更改可能会产生许多错误和警告，需要修复它们并再次生成项目。 此外，如果 Visual Studio 以后不支持特定的 `ToolsVersion`，那么打开项目会触发项目迁移过程，这是因为必须更改 `ToolsVersion` 值。 在这种情况下，该特定项目类型的子系统确切地知道要更改的内容，并且可以按前文所述自动完成更改。

## <a name="next-steps"></a>后续步骤

如需进一步讨论，请参阅以下文章：

- [ToolsVersion 指南](../msbuild/msbuild-toolset-toolsversion.md)
- [Framework 目标指南](../ide/visual-studio-multi-targeting-overview.md)

## <a name="see-also"></a>请参阅

[Visual Studio 2017 的项目迁移和升级参考](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects?view=vs-2017)

::: moniker-end
