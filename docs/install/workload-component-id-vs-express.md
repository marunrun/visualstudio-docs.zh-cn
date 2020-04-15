---
title: Visual Studio Desktop Express 工作负载和组件 ID
titleSuffix: ''
description: 使用工作负载和组件 ID 通过命令行安装 Visual Studio 或指定为 VSIX 清单中的依赖项
keywords: ''
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.date: 11/13/2018
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.assetid: a3c0cc76-e3ce-435c-a1af-a6318b5a4dbe
ms.prod: visual-studio-windows
ms.technology: vs-installation
monikerRange: vs-2017
open_to_public_contributors: false
ms.openlocfilehash: 1e24f90f24921bee9a6132ccc047c0b9da37fc90
ms.sourcegitcommit: 22deb247ad951e4971f27fdab413b158415d0584
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81276287"
---
# <a name="visual-studio-desktop-express-component-directory"></a>Visual Studio Desktop Express 组件目录

本页的表中列出了可用于通过使用命令行安装 Visual Studio 或可指定为 VSIX 清单中的依赖项的 ID。 请注意，我们将在发布 Visual Studio 更新时添加其他组件。

另请注意以下有关本页的注意事项：

* 每个工作负载均有其自己的部分，后跟工作负载 ID 和适用于工作负载的组件表格。
* 默认情况下，安装工作负载时将安装**必需**组件。
* 如果愿意，还可以安装**推荐**和**可选**组件。
* 我们还添加了一个部分，此部分列出了不属于任何工作负载的其他组件。

在 VSIX 清单中设置依赖项时，必须仅指定组件 ID。 使用本页中的表格来确定最小组件依赖项。 在某些情况下，这可能意味着仅从工作负载指定一个组件。 在其他情况下，这可能意味着你从单个工作负载指定多个组件或从多个工作负载指定多个组件。 有关详细信息，请参阅[如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md) 页。

有关如何使用这些 ID 的详细信息，请参阅[使用命令行参数安装 Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md) 页。 另外，有关其他产品的工作负载和组件 ID 的列表，请参阅 [Visual Studio 2017 工作负载和组件 ID](workload-and-component-ids.md) 页。

## <a name="express-for-windows-desktop"></a>Express for Windows Desktop

**ID：** Microsoft.VisualStudio.Workload.WDExpress

**说明：** 通过语法感知代码编辑、源代码管理和工作项管理，生成原生和托管应用，如 WPF、WinForms 和 Win32。 现已支持 C#、Visual Basic 和 Visual C++。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | 名称 | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.HelpViewer | 帮助查看器 | 15.6.27323.2 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Component.VC.Runtime.OSSupport | 适用于 UWP 的 Visual C++ 运行时 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio 核心编辑器 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server 命令行实用工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 15.0.26621.2 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必需
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.VC.CLI.Support | C++/CLI 支持 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.VC.Tools.ARM | 用于 ARM 的 Visual C++ 编译器和库 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | 用于 ARM64 的 Visual C++ 编译器和库 | 15.9.28230.55 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.8.27924.0 | 必需

## <a name="unaffiliated-components"></a>独立组件

这些组件不随附于任何工作负载，但可选择作为单个组件。

组件 ID | 名称 | Version
--- | --- | ---
n/a | n/a | n/a

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [命令行参数示例](command-line-parameter-examples.md)
* [创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)
