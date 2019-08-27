---
title: Visual Studio Community 2017 工作负载和组件 ID
titleSuffix: ''
description: 使用工作负载和组件 ID 通过命令行安装 Visual Studio 或指定为 VSIX 清单中的依赖项
keywords: ''
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.date: 2/12/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: dbc7fa1f5b931a598a607ce76cfe5c7f336e8ee2
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68177690"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-community-2017"></a>Visual Studio 核心编辑器（Visual Studio Community 2017 随附）

**ID：** Microsoft.VisualStudio.Workload.CoreEditor

**描述：** Visual Studio 核心 shell 体验，包括语法感知代码编辑、源代码管理和工作项管理。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio 核心编辑器 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | C++ 用户的 Visual Studio 起始页 | 15.0.27128.1 | Optional

## <a name="azure-development"></a>Azure 开发

**ID：** Microsoft.VisualStudio.Workload.Azure

**描述：** 用于开发云应用、创建资源以及生成包括 Docker 支持的容器的 Azure SDK、工具和项目。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | 必需
Component.Microsoft.VisualStudio.Web.AzureFunctions | Microsoft Azure WebJobs 工具 | 15.7.27617.1 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | 必需
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Component.NetFX.Core.Runtime | .NET Core 运行时 | 15.0.26208.0 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 15.9.28307.421 | 必需
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 15.9.28307.421 | 必需
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | 必需
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 15.9.28307.421 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
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
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Azure 开发必备组件 | 15.9.28107.0 | 必需
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Microsoft Azure WebJobs 工具 | 15.7.27617.1 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake 和流分析工具 | 15.9.28107.0 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.AspNet45 | 高级 ASP.NET 功能 | 15.7.27625.0 | 建议
Microsoft.VisualStudio.Component.Azure.MobileAppsSdk | Azure 移动应用 SDK | 15.7.27625.0 | 建议
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Azure 资源管理器核心工具 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Service Fabric 工具 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 15.7.27617.1 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Azure 云服务工具 | 15.0.26504.0 | 建议
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Azure 资源管理器工具 | 15.0.27005.2 | 建议
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 开发工具 | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 版开发工具 | 15.6.27406.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 开发工具 | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.Web | .NET Core 2.0 开发工具 | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | Azure 存储 AzCopy | 15.0.26906.1 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Optional

## <a name="data-storage-and-processing"></a>数据存储和处理

**ID：** Microsoft.VisualStudio.Workload.Data

**描述：** 使用 SQL Server、Azure Data Lake 或 Hadoop 连接、开发和测试数据解决方案。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | 建议
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | 建议
Component.Redgate.SQLSearch.VSExtension | Redgate SQL Search | 3.1.7.2062 | 建议
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 建议
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake 和流分析工具 | 15.9.28107.0 | 建议
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 建议
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 15.6.27406.0 | 建议
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 15.9.28307.421 | 建议
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 15.9.28307.421 | 建议
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 15.9.28125.51 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 15.7.27617.1 | 建议
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | 建议
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | 建议
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 建议
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 建议
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server 命令行实用工具 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 15.0.26621.2 | 建议
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 建议
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 建议
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 15.8.27825.0 | Optional

## <a name="data-science-and-analytical-applications"></a>数据科学和分析应用程序

**ID：** Microsoft.VisualStudio.Workload.DataScience

**描述：** 用于创建数据科学应用程序的语言和工具，包括 Python、R 和 F#。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Anaconda3.x64 | Anaconda3（64 位）(5.2.0) | 5.2.0 | 建议
Microsoft.Component.CookiecutterTools | Cookiecutter 模板支持 | 15.0.26621.2 | 建议
Microsoft.Component.PythonTools | Python 语言支持 | 15.0.26823.1 | 建议
Microsoft.Component.PythonTools.Web | Python Web 支持 | 15.9.28107.0 | 建议
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 建议
Microsoft.VisualStudio.Component.R.Open | Microsoft R 客户端 (3.3.2) | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.RHost | R 开发工具运行时支持 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.RTools | R 语言支持 | 15.0.26919.1 | 建议
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 建议
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 建议
Component.Anaconda2.x64 | Anaconda2（64 位）(5.2.0) | 5.2.0 | Optional
Component.Anaconda2.x86 | Anaconda2（32 位）(5.2.0) | 5.2.0 | Optional
Component.Anaconda3.x86 | Anaconda3（32 位）(5.2.0) | 5.2.0 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 15.6.27309.0 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python 本机开发工具 | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Win81 | 图形工具 Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.140 | 适用于桌面的 VC++ 2015.3 v14.00 (v140) 工具集 | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 15.0.26823.1 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional

## <a name="net-desktop-development"></a>.NET 桌面开发

**ID：** Microsoft.VisualStudio.Workload.ManagedDesktop

**描述：** 使用 C#、Visual Basic 和 F# 生成 WPF、Windows 窗体和控制台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET 桌面开发工具 | 15.7.27625.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 15.0.27005.2 | 建议
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 15.6.27406.0 | 建议
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 15.0.26208.0 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | Optional
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | Optional
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Optional
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 开发工具 | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 开发工具 | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | Optional
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server 命令行实用工具 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 15.0.26621.2 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | Optional
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | Optional

## <a name="game-development-with-unity"></a>使用 Unity 的游戏开发

**ID：** Microsoft.VisualStudio.Workload.ManagedGame

**描述：** 使用 Unity（功能强大的跨平台开发环境）创建 2D 和 3D 游戏。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 开发工具 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.Unity | Visual Studio Tools for Unity | 15.7.27617.1 | 必需
Component.UnityEngine.x64 | Unity 2018.3（64 位）编辑器 | 15.9.28307.271 | 建议
Component.UnityEngine.x86 | Unity 5.6 32 位编辑器 | 15.6.27406.0 | 建议

## <a name="linux-development-with-c"></a>使用 C++ 的 Linux 开发

**ID：** Microsoft.VisualStudio.Workload.NativeCrossPlat

**描述：** 创建和调试在 Linux 环境中运行的应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.MDD.Linux | 适用于 Linux 开发的 Visual C++ | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 15.6.27406.0 | 必需
Component.Linux.CMake | 用于 CMake 和 Linux 的 Visual C++ 工具 | 15.9.28307.102 | 建议
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 建议
Component.MDD.Linux.GCC.arm | 嵌入和 IoT 开发 | 15.6.27309.0 | Optional

## <a name="desktop-development-with-c"></a>使用 C++ 的桌面开发

**ID：** Microsoft.VisualStudio.Workload.NativeDesktop

**描述：** 使用 Microsoft C++ 工具集、ATL 或 MFC 生成 Windows 桌面应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Visual C++ 2017 Redistributable 更新 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | Visual C++ 核心桌面功能 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 15.0.27005.2 | 建议
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Graphics.Win81 | 图形工具 Windows 8.1 SDK | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 建议
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.VC.ATL | 用于 x86 和 x64 的 Visual C++ ATL | 15.7.27625.0 | 建议
Microsoft.VisualStudio.Component.VC.CMake.Project | 适用于 CMake 的 Visual C++ 工具 | 15.9.28307.102 | 建议
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 15.0.26823.1 | 建议
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Boost.Test 测试适配器 | 15.8.27906.1 | 建议
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Google Test 测试适配器 | 15.8.27906.1 | 建议
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 建议
Component.Incredibuild | IncrediBuild - 生成加速 | 15.7.27617.1 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 15.6.27309.0 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.140 | 适用于桌面的 VC++ 2015.3 v14.00 (v140) 工具集 | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | 用于 x86 和 x64 的 Visual C++ MFC | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.VC.CLI.Support | C++/CLI 支持 | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | 标准库模块（试验） | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | Windows 10 SDK (10.0.10240.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | 适用于桌面 C++ [x86 和 x64] 的 Windows 10 SDK (10.0.15063.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | 适用于 UWP 的 Windows 10 SDK (10.0.15063.0)：C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | 适用于 UWP 的 Windows 10 SDK (10.0.15063.0)：C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | 适用于桌面 C++ [x86 和 x64] 的 Windows 10 SDK (10.0.16299.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | 适用于桌面 C++ [ARM 和 ARM64] 的 Windows 10 SDK (10.0.16299.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | 适用于 UWP 的 Windows 10 SDK (10.0.16299.0)：C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | 适用于 UWP 的 Windows 10 SDK (10.0.16299.0)：C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.WinXP | 针对 C++ 的 Windows XP 支持 | 15.8.27924.0 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 | Windows 8.1 SDK 和 UCRT SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.WinXP | 针对 C++ 的 Windows XP 支持 | 15.8.27705.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | Windows 10 SDK (10.0.15063.0) | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 15.8.27825.0 | Optional

## <a name="game-development-with-c"></a>使用 C++ 的游戏开发

**ID：** Microsoft.VisualStudio.Workload.NativeGame

**描述：** 以 DirectX、Unreal 或 Cocos2d 为后盾，利用 C++ 的强大功能生成专业游戏。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Visual C++ 2017 Redistributable 更新 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | 必需
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Graphics.Win81 | 图形工具 Windows 8.1 SDK | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 15.0.26823.1 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 建议
Component.Android.NDK.R12B | Android NDK (R12B) | 12.1.10 | Optional
Component.Android.SDK23.Private | Android SDK 安装（API 级别 23）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28016.0 | Optional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Optional
Component.Cocos | Cocos | 15.0.26906.1 | Optional
Component.Incredibuild | IncrediBuild - 生成加速 | 15.7.27617.1 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Optional
Component.MDD.Android | C++ Android 开发工具 | 15.0.26606.0 | Optional
Component.OpenJDK | Microsoft distribution OpenJDK | 15.9.28125.51 | Optional
Component.Unreal | Unreal 引擎安装程序 | 15.8.27729.1 | Optional
Component.Unreal.Android | Visual Studio Android 支持 Unreal Engine | 15.9.28307.341 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 15.6.27309.0 | Optional
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 15.9.28016.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | Windows 10 SDK (10.0.10240.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | 适用于桌面 C++ [x86 和 x64] 的 Windows 10 SDK (10.0.15063.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | 适用于 UWP 的 Windows 10 SDK (10.0.15063.0)：C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | 适用于 UWP 的 Windows 10 SDK (10.0.15063.0)：C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | 适用于桌面 C++ [x86 和 x64] 的 Windows 10 SDK (10.0.16299.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | 适用于桌面 C++ [ARM 和 ARM64] 的 Windows 10 SDK (10.0.16299.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | 适用于 UWP 的 Windows 10 SDK (10.0.16299.0)：C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | 适用于 UWP 的 Windows 10 SDK (10.0.16299.0)：C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 | Windows 8.1 SDK 和 UCRT SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | Windows 10 SDK (10.0.15063.0) | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 15.8.27825.0 | Optional

## <a name="mobile-development-with-c"></a>使用 C++ 的移动开发

**ID：** Microsoft.VisualStudio.Workload.NativeMobile

**描述：** 使用 C++ 生成适用于 iOS、Android 或 Windows 的跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Android.SDK19.Private | Android SDK 安装（API 级别 19）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28107.0 | 必需
Component.Android.SDK21.Private | Android SDK 安装（API 级别 21）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28016.0 | 必需
Component.Android.SDK22.Private | Android SDK 安装（API 级别 22）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28016.0 | 必需
Component.Android.SDK23.Private | Android SDK 安装（API 级别 23）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28016.0 | 必需
Component.Android.SDK25.Private | Android SDK 安装（API 级别 25）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28016.0 | 必需
Component.OpenJDK | Microsoft distribution OpenJDK | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | 必需
Component.Android.NDK.R15C | Android NDK (R15C) | 15.2.1 | 建议
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 建议
Component.MDD.Android | C++ Android 开发工具 | 15.0.26606.0 | 建议
Component.Android.NDK.R12B | Android NDK (R12B) | 12.1.10 | Optional
Component.Android.NDK.R12B_3264 | Android NDK (R12B)（32 位） | 12.1.11 | Optional
Component.Android.NDK.R13B | Android NDK (R13B) | 13.1.7 | Optional
Component.Android.NDK.R13B_3264 | Android NDK (R13B)（32 位） | 13.1.8 | Optional
Component.Android.NDK.R15C_3264 | Android NDK (R15C)（32 位） | 15.2.1 | Optional
Component.Google.Android.Emulator.API23.Private | Google Android Emulator（API 级别 23）（本地安装） | 15.6.27413.0 | Optional
Component.HAXM.Private | Intel 硬件加速执行管理器 (HAXM)（本地安装） | 15.9.28307.421 | Optional
Component.Incredibuild | IncrediBuild - 生成加速 | 15.7.27617.1 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Optional
Component.MDD.IOS | C++ iOS 开发工具 | 15.0.26621.2 | Optional

## <a name="net-core-cross-platform-development"></a>.NET Core 跨平台开发

**ID：** Microsoft.VisualStudio.Workload.NetCoreTools

**描述：** 使用 .NET Core、ASP.NET Core、HTML/JavaScript 和包括 Docker 支持的容器生成跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | 必需
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | 必需
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 15.9.28307.421 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
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
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Component.Microsoft.VisualStudio.Web.AzureFunctions | Microsoft Azure WebJobs 工具 | 15.7.27617.1 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 15.9.28307.421 | 建议
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 15.9.28307.421 | 建议
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 15.9.28125.51 | 建议
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Microsoft Azure WebJobs 工具 | 15.7.27617.1 | 建议
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | 用于 Web 开发的云工具 | 15.8.27729.1 | 建议
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 版开发工具 | 15.6.27406.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 开发工具 | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.Web | .NET Core 2.0 开发工具 | 15.7.27625.0 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 开发时 IIS 支持 | 15.9.28219.51 | Optional

## <a name="mobile-development-with-net"></a>使用 .NET 的移动开发

**ID：** Microsoft.VisualStudio.Workload.NetCrossPlat

**描述：** 使用 Xamarin 生成适用于 iOS、Android 或 Windows 的跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Xamarin | Xamarin | 15.8.27906.1 | 必需
Component.Xamarin.RemotedSimulator | Xamarin 远程模拟器 | 15.6.27323.2 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 开发工具 | 15.6.27406.0 | 必需
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 开发工具 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.Merq | 常见 Xamarin 内部工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.MonoDebugger | Mono 调试程序 | 15.0.26720.2 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | ASP.NET 模板化引擎 | 15.8.27729.1 | 必需
Component.Android.SDK27 | Android SDK 安装程序（API 级别 27） | 15.9.28016.0 | 建议
Component.Google.Android.Emulator.API27 | Google Android 仿真程序（API 级别 27） | 15.9.28307.421 | 建议
Component.HAXM | Intel 硬件加速执行管理器 (HAXM)（全局安装） | 15.9.28307.421 | 建议
Component.OpenJDK | Microsoft distribution OpenJDK | 15.9.28125.51 | 建议
Component.Xamarin.Inspector | Xamarin Workbooks | 15.0.26606.0 | Optional
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | Optional
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.Graphics | 图像和 3D 模型编辑器 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | 适用于 Xamarin 的通用 Windows 平台工具 | 15.9.28307.102 | Optional

## <a name="aspnet-and-web-development"></a>ASP.NET 和 Web 开发

**ID：** Microsoft.VisualStudio.Workload.NetWeb

**描述：** 使用 ASP.NET、ASP.NET Core、HTML/JavaScript 和包括 Docker 支持的容器生成 Web 应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | 必需
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | 必需
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 15.9.28307.421 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
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
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Component.Microsoft.VisualStudio.Web.AzureFunctions | Microsoft Azure WebJobs 工具 | 15.7.27617.1 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | 建议
Microsoft.VisualStudio.Component.AspNet45 | 高级 ASP.NET 功能 | 15.7.27625.0 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 15.9.28307.421 | 建议
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 15.9.28307.421 | 建议
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 15.9.28125.51 | 建议
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Microsoft Azure WebJobs 工具 | 15.7.27617.1 | 建议
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | 用于 Web 开发的云工具 | 15.8.27729.1 | 建议
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 开发工具 | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK | .NET Core 2.0 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.Core.Component.SDK.1x | .NET Core 1.0 - 1.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.NetCore.1x.ComponentGroup.Web | .NET Core 1.0 - 1.1 Web 版开发工具 | 15.6.27406.0 | Optional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | .NET Core 2.0 开发工具 | 15.8.27729.1 | Optional
Microsoft.NetCore.ComponentGroup.Web | .NET Core 2.0 开发工具 | 15.7.27625.0 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 开发时 IIS 支持 | 15.9.28219.51 | Optional
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 15.6.27406.0 | Optional

## <a name="nodejs-development"></a>Node.js 开发

**ID：** Microsoft.VisualStudio.Workload.Node

**描述：** 使用 Node.js（一个由异步事件驱动的 JavaScript 运行时）生成可缩放的网络应用程序。 

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.Node.Build | Node.js MSBuild 支持 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.Node.Tools | Node.js 开发支持 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.TestTools.Core | 测试工具核心功能 | 15.7.27520.0 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | Optional

## <a name="officesharepoint-development"></a>Office/SharePoint 开发

**ID：** Microsoft.VisualStudio.Workload.Office

**描述：** 使用 C#、VB 和 JavaScript 创建 Office 和 SharePoint 外接程序、SharePoint 解决方案和 VSTO 外接程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | 必需
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | 必需
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET 桌面开发工具 | 15.7.27625.0 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.Sharepoint.Tools | Visual Studio 的 Office 开发工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server 命令行实用工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 15.0.26621.2 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | 必需
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 15.8.27825.0 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.TeamOffice | Visual Studio Tools for Office (VSTO) | 15.7.27625.0 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 15.8.27825.0 | Optional
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | .NET Framework 4.7.2 开发工具 | 15.8.27825.0 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 15.6.27406.0 | Optional

## <a name="python-development"></a>Python 开发

**ID：** Microsoft.VisualStudio.Workload.Python

**描述：** 对 Python 进行编辑、调试、交互式开发和源代码管理。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 语言支持 | 15.0.26823.1 | 必需
Component.CPython3.x64 | Python 3（64 位）(3.6.6) | 3.6.6 | 建议
Microsoft.Component.CookiecutterTools | Cookiecutter 模板支持 | 15.0.26621.2 | 建议
Microsoft.Component.PythonTools.Web | Python Web 支持 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 15.9.28107.0 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 建议
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 建议
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 建议
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 15.8.27729.1 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 建议
Component.Anaconda2.x64 | Anaconda2（64 位）(5.2.0) | 5.2.0 | Optional
Component.Anaconda2.x86 | Anaconda2（32 位）(5.2.0) | 5.2.0 | Optional
Component.Anaconda3.x64 | Anaconda3（64 位）(5.2.0) | 5.2.0 | Optional
Component.Anaconda3.x86 | Anaconda3（32 位）(5.2.0) | 5.2.0 | Optional
Component.CPython2.x64 | Python 2（64 位）(2.7.14) | 2.7.14 | Optional
Component.CPython2.x86 | Python 2（32 位）(2.7.14) | 2.7.14 | Optional
Component.CPython3.x86 | Python 3（32 位）(3.6.6) | 3.6.6 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 15.0.26720.2 | Optional
Component.Microsoft.Web.LibraryManager | 库管理器 | 15.8.27705.0 | Optional
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Optional
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | Optional
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Optional
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | Optional
Microsoft.Component.PythonTools.UWP | Python IoT 支持 | 15.0.26606.0 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 15.6.27309.0 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python 本机开发工具 | 15.9.28307.102 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | Optional
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 15.9.28307.421 | Optional
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 15.9.28307.421 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 15.9.28125.51 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 15.8.27906.1 | Optional
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.Graphics | 图像和 3D 模型编辑器 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Win81 | 图形工具 Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | Optional
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CMDUtils | SQL Server 命令行实用工具 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 15.0.26621.2 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 15.9.28107.0 | Optional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VC.140 | 适用于桌面的 VC++ 2015.3 v14.00 (v140) 工具集 | 15.7.27617.1 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 15.0.26823.1 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows81SDK | Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 15.9.28219.51 | Optional

## <a name="universal-windows-platform-development"></a>通用 Windows 平台开发

**ID：** Microsoft.VisualStudio.Workload.Universal

**描述：** 使用 C#、VB、JavaScript 或可选的 C++ 为通用 Windows 平台创建应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | 必需
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 开发工具 | 15.8.27924.0 | 必需
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.Graphics | 图像和 3D 模型编辑器 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.Component.UWP.Support | 通用 Windows 平台工具 | 15.9.28119.51 | 必需
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.Cordova | 适用于 Cordova 的通用 Windows 平台工具 | 15.9.28307.102 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET 本机和 .NET 标准 | 15.8.27906.1 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | 适用于 Xamarin 的通用 Windows 平台工具 | 15.9.28307.102 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Microsoft.Component.VC.Runtime.OSSupport | 适用于 UWP 的 Visual C++ 运行时 | 15.6.27406.0 | Optional
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Graphics.Win81 | 图形工具 Windows 8.1 SDK | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Phone.Emulator.15254 | Windows 10 移动版仿真程序（秋季创意者更新） | 15.0.27406.0 | Optional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | 适用于 ARM64 的 C++ 通用 Windows 平台工具 | 15.0.28125.51 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM | 用于 ARM 的 Visual C++ 编译器和库 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | 用于 ARM64 的 Visual C++ 编译器和库 | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | Windows 10 SDK (10.0.10240.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | Windows 10 SDK (10.0.10586.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | Windows 10 SDK (10.0.14393.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | 适用于桌面 C++ [x86 和 x64] 的 Windows 10 SDK (10.0.15063.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | 适用于 UWP 的 Windows 10 SDK (10.0.15063.0)：C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | 适用于 UWP 的 Windows 10 SDK (10.0.15063.0)：C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | 适用于桌面 C++ [x86 和 x64] 的 Windows 10 SDK (10.0.16299.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | 适用于桌面 C++ [ARM 和 ARM64] 的 Windows 10 SDK (10.0.16299.0) | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | 适用于 UWP 的 Windows 10 SDK (10.0.16299.0)：C#、VB、JS | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | 适用于 UWP 的 Windows 10 SDK (10.0.16299.0)：C++ | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | USB 设备连接性 | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ 通用 Windows 平台工具 | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | Windows 10 SDK (10.0.15063.0) | 15.8.27825.0 | Optional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 15.8.27825.0 | Optional

## <a name="visual-studio-extension-development"></a>Visual Studio 扩展开发

**ID：** Microsoft.VisualStudio.Workload.VisualStudioExtension

**描述：** 为 Visual Studio 创建加载项和扩展，包括新命令、代码分析器和工具窗口。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | 必需
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | 必需
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 15.6.27406.0 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET framework 4.6.1 开发工具 | 15.8.27825.0 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 15.9.28016.0 | 必需
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 15.6.27309.0 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.Static.Analysis.Tools | 静态分析工具 | 15.0.26208.0 | 必需
Microsoft.VisualStudio.Component.VSSDK | Visual Studio SDK | 15.8.27729.1 | 必需
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Visual Studio 扩展开发必备组件 | 15.7.27625.0 | 必需
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | 建议
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 15.0.26208.0 | 建议
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 15.0.26208.0 | Optional
Microsoft.Component.CodeAnalysis.SDK | .NET 编译器平台 SDK | 15.0.27729.1 | Optional
Microsoft.Component.VC.Runtime.OSSupport | 适用于 UWP 的 Visual C++ 运行时 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.DslTools | 建模 SDK | 15.0.27005.2 | Optional
Microsoft.VisualStudio.Component.VC.ATL | 用于 x86 和 x64 的 Visual C++ ATL | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | 用于 x86 和 x64 的 Visual C++ MFC | 15.7.27625.0 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | Visual Studio C++ 核心功能 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | VC++ 2017 版本 15.9 v14.16 最新 v141 工具 | 15.9.28230.55 | Optional

## <a name="mobile-development-with-javascript"></a>使用 JavaScript 的移动开发

**ID：** Microsoft.VisualStudio.Workload.WebCrossPlat

**描述：** 使用用于 Apache Cordova 的工具生成 Android、iOS 和 UWP 应用。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.CordovaToolset.6.3.1 | Cordova 6.3.1 工具集 | 15.7.27625.0 | 必需
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | 必需
Microsoft.VisualStudio.Component.Cordova | 使用 JavaScript 核心功能的移动开发 | 15.0.26606.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.ProjectSystem | JavaScript ProjectSystem 和共享工具 | 15.0.26606.0 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 15.9.28125.51 | 必需
Microsoft.VisualStudio.Component.TypeScript.2.3 | TypeScript 2.3 SDK | 15.8.27729.1 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.1 | TypeScript 3.1 SDK | 15.0.28218.60 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 15.8.27825.0 | 必需
Component.Android.SDK23.Private | Android SDK 安装（API 级别 23）（用于 JavaScript/C++ 的移动开发的本地安装） | 15.9.28016.0 | Optional
Component.Google.Android.Emulator.API23.Private | Google Android Emulator（API 级别 23）（本地安装） | 15.6.27413.0 | Optional
Component.HAXM.Private | Intel 硬件加速执行管理器 (HAXM)（本地安装） | 15.9.28307.421 | Optional
Component.OpenJDK | Microsoft distribution OpenJDK | 15.9.28125.51 | Optional
Microsoft.Component.ClickOnce | ClickOnce 发布 | 15.8.27825.0 | Optional
Microsoft.Component.NetFX.Native | .NET Native | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 15.8.27825.0 | Optional
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 15.8.27729.1 | Optional
Microsoft.VisualStudio.Component.Git | 用于 Windows 的 Git | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.Graphics | 图像和 3D 模型编辑器 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Phone.Emulator.15254 | Windows 10 移动版仿真程序（秋季创意者更新） | 15.0.27406.0 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 15.0.26208.0 | Optional
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 15.6.27406.0 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 15.9.28307.102 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.Cordova | 适用于 Cordova 的通用 Windows 平台工具 | 15.9.28307.102 | Optional

## <a name="unaffiliated-components"></a>独立组件

这些组件不随附于任何工作负载，但可选择作为单个组件。

组件 ID | name | Version
--- | --- | ---
Component.Android.Emulator | 适用于 Android 的 Visual Studio 仿真程序 | 15.6.27413.0
Component.Android.NDK.R11C | Android NDK (R11C) | 11.3.14
Component.Android.NDK.R11C_3264 | Android NDK (R11C)（32 位） | 11.3.16
Component.Android.SDK23 | Android SDK 安装程序（API 级别 23）（全局安装） | 15.9.28107.0
Component.Android.SDK25 | Android SDK 安装程序（API 级别 25） | 15.9.28107.0
Component.GitHub.VisualStudio | 适用于 Visual Studio 的 GitHub 扩展 | 2.5.2.2500
Component.Google.Android.Emulator.API23.V2 | Google Android Emulator（API 级别 23）（全局安装） | 15.6.27413.0
Component.Google.Android.Emulator.API25 | Google Android Emulator（API 级别 25） | 15.7.27604.0
Microsoft.Component.Blend.SDK.WPF | 用于 .NET 的 Blend for Visual Studio SDK | 15.6.27406.0
Microsoft.Component.HelpViewer | 帮助查看器 | 15.9.28307.421
Microsoft.VisualStudio.Component.DependencyValidation.Community | 依赖项验证 | 15.0.26208.0
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 15.0.27005.2
Microsoft.VisualStudio.Component.LinqToSql | LINQ to SQL 工具 | 15.6.27406.0
Microsoft.VisualStudio.Component.Phone.Emulator | Windows 10 移动版仿真程序（周年纪念版） | 15.6.27406.0
Microsoft.VisualStudio.Component.Phone.Emulator.15063 | Windows 10 Mobile 仿真器（创意者更新） | 15.6.27406.0
Microsoft.VisualStudio.Component.Runtime.Node.x86.6.4.0 | 基于 Node.js v6.4.0 (x86) 的组件运行时 | 15.7.27617.1
Microsoft.VisualStudio.Component.Runtime.Node.x86.7.4.0 | 基于 Node.js v7.4.0 (x86) 的组件运行时 | 15.7.27617.1
Microsoft.VisualStudio.Component.TypeScript.2.0 | TypeScript 2.0 SDK | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.1 | TypeScript 2.1 SDK | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.2 | TypeScript 2.2 SDK | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.5 | TypeScript 2.5 SDK | 15.6.27406.0
Microsoft.VisualStudio.Component.TypeScript.2.6 | TypeScript 2.6 SDK | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.7 | TypeScript 2.7 SDK | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.8 | TypeScript 2.8 SDK | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.9 | TypeScript 2.9 SDK | 15.0.27924.0
Microsoft.VisualStudio.Component.TypeScript.3.0 | TypeScript 3.0 SDK | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.ATL.ARM | Visual C++ ATL for ARM | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | 带有 Spectre 缓解措施的 Visual C++ ATL for ARM | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | Visual C++ ATL for ARM64 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的 Visual C++ ATL for ARM64 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.Spectre | 带有 Spectre 缓解措施的 Visual C++ ATL (x86/x64) | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | 带有 Spectre 缓解措施的 Visual C++ MFC for x86/x64 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ClangC2 | Clang/C2（实验） | 15.7.27520.0
Microsoft.VisualStudio.Component.VC.MFC.ARM | Visual C++ MFC for ARM | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | 带有 Spectre 缓解措施的 Visual C++ MFC for ARM | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | Visual C++ MFC for ARM64 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的针对 ARM64 的 Visual C++ MFC 支持 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | 面向 Spectre 的 VC++ 2017 版本 15.9 v14.16 库 (ARM) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | 面向 Spectre 的 VC++ 2017 版本 15.9 v14.16 库 (ARM64) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | 面向 Spectre 的 VC++ 2017 版本 15.9 v14.16 库（x86 和 x64） | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Tools.14.11 | VC++ 2017 版本 15.4 v14.11 工具集 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.12 | VC++ 2017 版本 15.5 v14.12 工具集 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.13 | VC++ 2017 版本 15.6 v14.13 工具集 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.14 | VC++ 2017 版本 15.7 v14.14 工具集 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.15 | VC++ 2017 版本 15.8 v14.15 工具集 | 15.0.28230.55
