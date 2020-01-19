---
title: 移植、迁移和升级项目 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
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
ms.assetid: bee759bd-6ff5-4c2e-913a-ea7d3c906c29
caps.latest.revision: 108
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 3361b04900e549d037338abfba0911b232c9e1bd
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919094"
---
# <a name="port-migrate-and-upgrade-visual-studio-projects"></a>移植、迁移和升级 Visual Studio 项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅 [Visual Studio 的项目迁移和升级参考](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects)。

在考虑是否应迁移到较新版本的 Visual Studio 时，你可以参考本文来了解你在 Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 中创建的哪些解决方案、项目、文件和其他资产会在 Visual Studio 2013 和 Visual Studio 2015 中运行但不进行任何修改。 或者，当尝试打开的项目在打开过项目的 Visual Studio 版本中不受支持，或者该项目需要 SDK 或扩展名（如 Azure SDK for .NET）时，遇到一条错误消息，那么你可能已到达此页。

许多常用的资产在 Visual Studio 2015、Visual Studio 2013 和两个早期版本中的行为一致。 例如，在 Visual Studio 2015 中，你可以打开在 Visual Studio 2013 或 Visual Studio 2012 中创建的项目，对其进行更改，然后在 Visual Studio 2015 中将其重新打开。 将保留你的更改，并且项目的行为与早期版本中的行为一致。 上述情况同样适用于在 Visual Studio 2010 SP1 中创建的许多资产。

对于 Visual Basic，Visual Studio 2015 不会引入会阻止对 Visual Studio 2013 中创建的 Visual Basic 应用进行编译的更改。 使用 Visual Studio 2015 重新编译的 Visual Basic 应用的运行时行为不会更改。

如果将 Visual Studio 2015 与 Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 一起使用，则可在任意一个版本中创建和修改项目和文件。 可以在各个版本之间传输项目和文件，前提是不添加一个或多个版本不支持的功能。

## <a name="project"></a>项目

以下列表描述了 Visual Studio 2015 和 Visual Studio 2013 中对在 Visual Studio 2012 或 Visual Studio 2010 SP1 中创建的项目的支持。 使用此列表来帮助确定你是否可以在 Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 中“按原样”打开项目，或者是否必须修改项目以确保兼容性。

|项目类型|兼容性|
|---------------------|-------------------|
|通用 Windows 平台应用|若要在 Visual Studio 安装程序中安装通用 Windows 应用开发工具，请选择 **“自定义”** 或 **“修改”** ，然后选择 **“通用 Windows 应用程序开发工具”** 。<br /><br /> Windows 10 通用 Windows 平台 (UWP) 应用开发仅在 Windows 10 或 [!INCLUDE[win81](../includes/win81-md.md)] 上的 Visual Studio 2015 中受支持。|
|Windows 应用商店应用程序|Windows 应用商店应用开发（包括面向 Windows 8.1 和 Windows Phone 8.1 的通用应用）在 [!INCLUDE[win81](../includes/win81-md.md)] 和 Windows 10 中受支持。 现有的 [!INCLUDE[win8](../includes/win8-md.md)] 项目可以继续获得服务，但无法创建新的 [!INCLUDE[win8](../includes/win8-md.md)] 项目。 [!INCLUDE[win81](../includes/win81-md.md)]项目只能依赖于某些类型的引用。 有关详细信息，请参阅[管理项目中的引用](../ide/managing-references-in-a-project.md)。 **注意：** 使用 Visual Studio 2015 或 Visual Studio 2013 创建的 [!INCLUDE[win81](../includes/win81-md.md)] 项目无法在 Visual Studio 2012 中打开。 这是因为使用 Visual Studio 2015 和 Visual Studio 2013 创建的 [!INCLUDE[win81](../includes/win81-md.md)] 项目以这些版本为目标，而 Visual Studio 2012 仅支持以 [!INCLUDE[win8](../includes/win8-md.md)] 为目标的 [!INCLUDE[win8](../includes/win8-md.md)] 项目。|
|[!INCLUDE[net_v451](../includes/net-v451-md.md)]|在安装适当的多目标包之后，可以在 Visual Studio 2015 和 Visual Studio 2013 中创建并使用这些项目。 Visual Studio 2010 SP1 中不支持这些项目。|
|[!INCLUDE[net_v45](../includes/net-v45-md.md)]|可以在 Visual Studio 2015、Visual Studio 2013 和 Visual Studio 2012 中创建和打开这些项目，但在 Visual Studio 2010 SP1 中却不是如此。|
|BizTalk|BizTalk Server 项目与 Visual Studio 2015 或 Visual Studio 2013 不兼容。|
|C#/Visual Basic Silverlight 4 应用程序或类库|如果允许 Visual Studio 自动更新项目，则可以在 Visual Studio 2013 或 Visual Studio 2012 中打开该项目。|
|C#/Visual Basic Web 窗体或 Windows 窗体|可以在 Visual Studio 2013 和 Visual Studio 2012 中打开项目。|
|Visual Basic 6 和 Visual C++ 6|Visual Studio 2012 和 Visual Studio 2013 不支持调试使用 Visual Basic 6 或 Visual C++ 6 生成的应用程序；若要调试这些应用程序，请使用早期版本的 Visual Studio。|
|编码的 UI 测试|如果允许 Visual Studio 自动更新项目，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开该项目。|
|F#|如果允许 Visual Studio 升级在 Visual Studio 2010 SP1 中创建的项目，则可以在 Visual Studio 2013 和 Visual Studio 2012 中打开该项目。 但是，无法将在 Visual Studio 早期版本中创建的 Silverlight 项目升级到 Visual Studio 2013。 相反，你必须在 Visual Studio 2013 中创建一个 Silverlight 项目，然后将你的代码复制到其中。 在 Visual Studio 2013 中创建的 Silverlight 项目将以 Silverlight 5 为目标。|
|LightSwitch|如果允许 Visual Studio 自动升级项目，则只能在 Visual Studio 2013 中打开它。|
|本地数据库缓存|本地数据库缓存模板和“配置数据同步”  对话框未包括在 Visual Studio 2013 中。 如果安装了 Microsoft Synchronization Services v1.0，则可以使用 Visual Studio 2013 来打开并运行在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中创建的项目，但是，如果你想要在 Visual Studio 2013 中更新项目，则必须手动在代码中进行全部更改。 或者，可以继续使用 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 来维护和更新这些项目。  对于新开发，应以 Microsoft Sync Framework 提供的新的同步模型为目标。 有关信息，请参见 [Microsoft Sync Framework 开发人员中心](https://msdn.microsoft.com/sync/default)|
|模型视图控制器框架|Visual Studio 2010 SP1 仅支持 MVC 2 和 MVC 3，Visual Studio 2012 仅支持 MVC 3 和 MVC 4，Visual Studio 2013 仅支持 MVC 4。 有关如何从 MVC 2 自动升级到 MCV 3 的信息，请参阅 [ASP.NET MVC 3 应用程序升级程序](https://aspnet.codeplex.com/releases/view/59008)。 有关如何从 MVC 2 手动升级到 MVC 3 的信息，请参阅 [将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 Tools 更新](https://aspnet.codeplex.com/releases/view/59008)。 有关如何从 MVC3 手动升级到 MVC 4 的信息，请参阅 [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](/aspnet/whitepapers/mvc4-release-notes)。 如果你的项目以 .NET Framework 3.5 SP1 为目标，则必须重定目标以使用 .NET Framework 4。|
|建模|如果允许 Visual Studio 自动更新项目，则可以在 Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 中打开该项目。<br /><br /> Team Foundation 在生成建模项目时将会尝试验证项目中的层。 在 Visual Studio 2013 中，Team Foundation Build 无法验证在 Visual Studio 2010 SP1 中创建的建模项目中的层。 但是，在 Visual Studio 2010 SP1 中，Team Foundation Build 可以验证在 Visual Studio 2013 中创建的建模项目中的层。|
|MPI/群集调试|如果在运行 Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 的计算机上安装了相同版本的运行时或工具，则可以在所有这三个版本中打开此项目。|
|MSI 安装程序 (.vdproj)|你无法在 Visual Studio 2013 中打开此项目，因为它不支持该项目类型。 我们建议你使用 InstallShield Limited Edition for Visual Studio (ISLE)，这是一个直接支持大多数 Windows 平台和应用程序运行时的免费的部署解决方案。 你还可以使用 ISLE 从 Visual Studio 安装程序项目导入数据和设置。 中运行但不进行任何修改。|
|Office 2007 VSTO|如果你升级项目以面向 Office 2013 和 .NET Framework 4，则可以在 Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 中打开此项目。|
|Office 2010 VSTO|如果项目面向 .NET Framework 4，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。 所有其他项目需要单向升级。|
|丰富的 Internet 应用程序|如果升级项目，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。|
|SharePoint 2007|此项目不能在 Visual Studio 2013 中打开。 但是，如果你将项目手动升级到 SharePoint 2010，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开它。 有关如何升级 SharePoint 2007 的详细信息，请参阅[从 SharePoint 2007 迁移到 SharePoint 2010（针对 IT 专业人员）](https://channel9.msdn.com/Blogs/matthijs/Migrating-from-SharePoint-2007-to-SharePoint-2010-for-the-IT-Pro)和 [SharePoint Server 2010 的 SharePoint 企业搜索迁移工具](/previous-versions/office/developer/sharepoint-2010/ee556856(v%3Doffice.14))。|
|SharePoint 2010|可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。|
|SketchFlow|如果允许 Visual Studio 将项目升级到 WPF 4.5/Silverlight 5，则可以在 Visual Studio 2012 和 Visual Studio 2013 中打开它。|
|[!INCLUDE[ssKatmai_exp](../includes/sskatmai-exp-md.md)] 数据库|可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。 如果你有使用早期版本的 SQL Server 创建的数据库文件 (.mdf)，则必须将它升级为 [!INCLUDE[sql_Denali_long](../includes/sql-denali-long-md.md)] ，然后才能将它与 SQL Server Express LocalDB 一起使用，但该数据库不再与早期版本的 SQL Server 相兼容。 如果不升级，则可通过在同一计算机上安装和使用 [!INCLUDE[ssKatmai_exp](../includes/sskatmai-exp-md.md)] 来继续在 Visual Studio 2013 中使用该数据库。 有关详细信息，请参阅[升级 .mdf 文件](../data-tools/upgrade-dot-mdf-files.md)。|
|[!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] 学习版|如果在运行 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 的计算机上安装了 [!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] Express，则可以在这三个版本中打开项目。|
|SQL Server 报告项目|可以在 Visual Studio 2013 和 Visual Studio 2012 中打开项目。 对于仅限本地模式（即，在未连接到 SQL Server 时），你不会获得与 [!INCLUDE[vs2010](../includes/vs2010-md.md)]中的查看器相关联的控件的设计时体验，但是项目在运行时将正常工作。 **注意：** 如果添加 Visual Studio 2013 特定的功能，则报表架构将自动升级，并且你无法再在 Visual Studio 2012 中打开项目。|
|单元测试|可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中使用 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 打开在任何这些版本中创建的测试。|
|Visual C++|可以使用 Visual Studio 2013 打开在 Visual Studio 2012 或 Visual Studio 2010 SP1 中创建的 C++ 项目。 如果要使用 Visual Studio 2013 生成环境来生成在 Visual Studio 2012 中创建的项目，则必须在同一计算机上安装这两个版本的 Visual Studio。 有关详细信息，请参阅[如何：将 Visual C++ 项目升级到 Visual Studio 2015](../porting/how-to-upgrade-visual-cpp-projects-to-visual-studio-2015.md) 和 [Visual C++ 移植和升级指南](https://msdn.microsoft.com/library/f5fbcc3d-aa72-41a6-ad9a-a706af2166fb)。|
|Visual Studio 2010 网站|如果允许 Visual Studio 自动升级项目，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开该项目。|
|Visual Studio 2010 数据库 (.dbproj)|如果将项目转换为 SQL Server Data Tools 数据库项目，则可以在 Visual Studio 2013 中打开它。 但是，Visual Studio 2013 不支持下列项目：<br /><br /> - 单元测试<br />- 数据生成计划<br />- 数据比较文件<br />- 静态代码分析的自定义规则扩展<br />- server.sqlsettings<br />- .sqlcmd 文件<br />- 自定义部署扩展<br />- 分部项目 (.files)<br /><br /> 如果你安装了 SQL Server Data Tools，则可以在转换后在 Visual Studio 2010 SP1 中打开项目。 有关详细信息，请参阅 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)。|
|Visual Studio 2010 Visual Database Tools|可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。|
|Visual Studio 实验室管理工具版|可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中使用 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 打开在任何这些版本中创建的环境。 但在可以创建环境之前，Microsoft 测试管理器的版本必须与 Team Foundation Server 的版本匹配。|
|Visual Studio 宏|你无法在 Visual Studio 2013 中打开此项目，因为它不支持该项目类型。|
|Visual Studio SDK/VSIX|将 Visual Studio SDK 项目升级到 Visual Studio 2013 之后，无法在 Visual Studio 2012 中打开它。 有关详细信息，请参阅[如何：将扩展性项目迁移到 Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md)。|
|Microsoft Azure Tools for Visual Studio|如果你正在使用 Microsoft Azure Tools for Visual Studio 2.1 版，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。 对于面向早期版本的项目，如果你允许 Visual Studio 将项目升级到 2.1 版，则可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开它。|
|Windows Communication Foundation、Windows Presentation Foundation|可以在 Visual Studio 2013、Visual Studio 2012 和 Visual Studio 2010 SP1 中打开此项目。|
|Windows Mobile|你无法在 Visual Studio 2013 中打开此项目，因为它不支持该项目类型。|
|Windows Phone 7.1|如果允许 Visual Studio 将项目升级到 Windows Phone 8.0，则可以在 Visual Studio 2012 和 Visual Studio 2013 中打开它。|
|其他|可以在 Visual Studio 2012、Visual Studio 2013 和 Visual Studio 2010 SP1 中打开大多数其他项目类型。|
|Frontpage 网站|你无法在 Visual Studio 2013 中打开此项目，因为它不支持该项目类型。|
|可移植类库|如果允许 Visual Studio 自动更新项目，则可以在 Visual Studio 2013、Visual Studio 2012 或 Visual Studio 2010 SP1 中打开该项目。<br /><br /> - 以 Silverlight 4 为目标的项目将以 Silverlight 5 为目标。<br />- 以 Windows Phone 7.0 或 Windows Phone 7.5 的项目将以 Windows Phone 8 为目标。<br />- 以 Xbox 360 为目标的项目将不再以 Xbox 360 为目标。|
|Azure 项目，例如云服务项目（.ccproj 扩展名）和扩展名为.deployproj Azure 资源管理器项目（云部署项目）|若要打开这些类型的项目，请首先安装 [Azure SDK for .NET](https://azure.microsoft.com/downloads/)，然后打开该项目。|

## <a name="troubleshooting-project-compatibility-issues"></a>项目兼容性问题疑难解答
 当无法在 Visual Studio 2015 或 Visual Studio 2013 中打开项目时，可以进行以下操作：

- 如果你尝试打开一个项目，但是该项目在 Visual Studio 2015 或 Visual Studio 2013 中不受支持且未安装关联的 Visual Studio 版本，则可能会出现项目类型不受支持的消息，而该项目类型可能会在“不受支持的项目”下的“检查项目和解决方案更改”对话框中列出   。 若要解决此问题，可在 Windows 的 **“控制面板”** 中打开“程序和功能”页，选择 **“Visual Studio”** ，然后选择 **“更改”** 和 **“修复”** 。 然后，可以安装所缺少的版本。

- 如果尝试在 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] 中打开桌面应用的项目，会出现错误，显示以下消息中的其中一条：“此 Visual Studio 版本仅支持 [!INCLUDE[win81](../includes/win81-md.md)] 应用”或“此项目与 Visual Studio 的当前版本不兼容”。 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] 仅限于为 Windows 8.1 设计的 Windows 应用商店应用的开发、测试和部署。 若要打开桌面应用程序项目，必须使用支持该项目类型的 Visual Studio 版本。

   有关 Visual Studio 版本的详细信息，请参阅 [Microsoft Visual Studio 产品](https://visualstudio.microsoft.com/products/)

- 如果你尝试在 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] 桌面中打开 Windows 应用商店应用项目，则会发生错误。 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] 桌面无法用于生成 Windows 应用商店应用。 如果要生成 Windows 应用商店应用，则还可以安装 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)]。 或者，若要为所有 Microsoft 平台和网站开发应用，请尝试 Visual Studio Professional 2013。

- 如果项目需要 Visual Studio 2013 特定的功能，则无法在早期版本中打开它。

- 如果你正使用 Visual Studio 2012，并且要打开在 Visual Studio 2013 中创建的项目，则可能能够自定义项目系统以合并 Visual Studio 2013 的功能。 有关如何执行此操作的信息，请参阅[使自定义项目版本可区别](../misc/making-custom-projects-version-aware.md)。

  有关其他的疑难解答信息，请参阅 [Visual Studio 2013 兼容性](https://support.microsoft.com/help/2863286/roundtrip-issues-for-visual-studio-2012-and-visual-studio-2013-preview) 知识库文章。

## <a name="file"></a>文件

以下列表标识了 Visual Studio 2013 是否支持每个类型的文件、是否可以在 Visual Studio 2012 和 Visual Studio 2010 SP1 中打开文件以及是否必须修改它以确保兼容性。

|文件类型|兼容性|
|------------------|-------------------|
|AppManifest、Inbrowsersettings、OutOfBrowserSettings（.xml 文件）|可以在 Visual Studio 2012、Visual Studio 2013 和 Visual Studio 2010 SP1 中打开这些文件。|
|BizTalk 平面文件架构|可以将这些架构添加到 Visual Studio 2013 中的 BizTalk 2013 项目。 若要将 Visual Studio 2013 与具有平面文件架构的 BizTalk 2010 项目配合使用，请在安装了 Visual Studio 2013 的计算机上安装 BizTalk 2013。 首次打开 BizTalk 2010 项目时，它会自动升级到 BizTalk 2013 或 Visual Studio 2013 项目系统。|
|客户端报表定义 (.rdlc) 文件|你可以在 Visual Studio 2013 中打开这些文件，并且，如果你添加了 Visual Studio 2013 功能和控件，则将自动升级架构。|
|代码分析规则集|可以在 Visual Studio 2012、Visual Studio 2013 和 Visual Studio 2010 SP1 中打开这些文件。|
|数据层应用程序包文件|如果这些文件的版本是 2.0 或 2.5，则可以在 Visual Studio 2013 中打开这些文件。|
|调试器转储文件|可以在 Visual Studio 2012、Visual Studio 2013 和 Visual Studio 2010 SP1 中打开这些文件。|
|定向图形标记语言 (DGML) 关系图文件|可以在 Visual Studio 2012、Visual Studio 2013 和 Visual Studio 2010 SP1 中打开这些文件，而无需更改文件。|
|实体数据模型 (EDMX) 文件|在 Visual Studio 2013 中，可以打开以 .NET Framework 4.5 或 .NET Framework 4 为目标的 EDMX 文件，而不用对文件做任何更改。|
|探查器报告文件|可以在 Visual Studio 2012 和 Visual Studio 2013 中打开探查器报告文件（.vsp、.vsps、.psess 和 .vspf）。 不能在 Visual Studio 2010 SP1 中打开 .vspx 文件。|
|解决方案 (.suo) 文件|可以使用 Visual Studio 2013 打开在 Visual Studio 2012 或 Visual Studio 2010 SP1 中创建的解决方案文件|
|SQL Server Compact Edition|Visual Studio 2013 不支持 SQL Server Compact Edition。|
|SQLX 文件|若要在 Visual Studio 2013 中打开这些文件，必须执行单向升级，在 Visual Studio 的目标版本上部署 .sqlx 文件，然后以 .dacpac 格式重新生成文件。|
|来自 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 的 IntelliTrace 日志文件|可以在 Visual Studio 2012、Visual Studio 2013 和 Visual Studio 2010 SP1 中打开这些文件。|
|JavaScript 内存分析程序 (.diagsession) 文件|由 Visual Studio 早期版本创建的文件可在 Visual Studio 2013 中查看。 但是，根据收集的信息，在 Visual Studio 2013 中创建的文件可能无法在 Visual Studio 2012 或 Visual Studio 2010 SP1 中打开。|

## <a name="integration"></a>集成资产

如果你所使用的客户端和服务器的 Visual Studio Team Foundation Server 版本不同，则可能遇到兼容性问题。

|集成类型|兼容性|
|-------------------------|-------------------|
|代码评审和“我的工作”|如果将 [!INCLUDE[esprfound](../includes/esprfound-md.md)] 的客户端连接到 [!INCLUDE[vstsTfsRosarioLong](../includes/vststfsrosariolong-md.md)]，则“代码评审”和“我的工作”功能将不起作用。|
|[!INCLUDE[vs_dev11_expwin_long](../includes/vs-dev11-expwin-long-md.md)]|不能使用 64 位环境（如 MSBuild 或 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] ）来生成在 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 中创建的 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)]应用。|

## <a name="see-also"></a>请参阅

- [使自定义项目版本可区别](../misc/making-custom-projects-version-aware.md)
