---
title: Visual Studio Enterprise 2019 工作负载和组件 ID
titleSuffix: ''
description: 使用工作负载和组件 ID 通过命令行安装 Visual Studio 或指定为 VSIX 清单中的依赖项
keywords: ''
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.date: 12/03/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 58c7d8775a1db09d2628eb6946924ae3543b80e4
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74795746"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-enterprise-2019"></a>Visual Studio 核心编辑器（Visual Studio Enterprise 2019 随附）

**ID：** Microsoft.VisualStudio.Workload.CoreEditor

**描述：** Visual Studio 核心 shell 体验，包括语法感知代码编辑、源代码管理和工作项管理。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio 核心编辑器 | 16.1.28811.260 | 必需
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | C++ 用户的 Visual Studio 起始页 | 16.0.28315.86 | Optional

## <a name="azure-development"></a>Azure 开发

**ID：** Microsoft.VisualStudio.Workload.Azure

**描述：** 使用 .NET Core 和 .NET Framework 开发云应用和创建资源的 Azure SDK、工具和项目。 还包括用于容器化应用程序的工具，包括 Docker 支持。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | 必需
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs 工具 | 16.0.28714.129 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | 必需
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.NetCore.Component.DevelopmentTools | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.NetCore.Component.Web | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 16.1.28810.153 | 必需
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 16.4.29313.120 | 必需
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Azure 开发必备组件 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs 工具 | 16.0.28621.142 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 必需
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake 和流分析工具 | 16.4.29313.120 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 16.0.28516.191 | 建议
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 LTS 运行时 | 16.4.29519.181 | 建议
Microsoft.VisualStudio.Component.AspNet45 | 高级 ASP.NET 功能 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.Azure.Kubernetes.Tools | Visual Studio Tools for Kubernetes | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Azure.Powershell | Azure Powershell | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Azure 资源管理器核心工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Service Fabric 工具 | 16.4.29313.120 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 16.3.29207.166 | 建议
Microsoft.VisualStudio.Component.Debugger.Snapshot | 快照调试程序 | 16.2.29003.222 | 建议
Microsoft.VisualStudio.Component.Debugger.TimeTravel | 按时间顺序查看调试器 | 16.4.29511.114 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Azure 云服务工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Azure 资源管理器工具 | 16.0.28528.71 | 建议
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET framework 4.6.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 16.4.29318.151 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | Azure 存储 AzCopy | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional

## <a name="data-storage-and-processing"></a>数据存储和处理

**ID：** Microsoft.VisualStudio.Workload.Data

**描述：** 使用 SQL Server、Azure Data Lake 或 Hadoop 连接、开发和测试数据解决方案。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | 建议
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | 建议
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake 和流分析工具 | 16.4.29313.120 | 建议
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 16.0.28516.191 | 建议
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 16.1.28810.153 | 建议
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 16.4.29313.120 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 16.3.29207.166 | 建议
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | 建议
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 建议
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 建议
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 建议
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 16.0.28315.86 | Optional

## <a name="data-science-and-analytical-applications"></a>数据科学和分析应用程序

**ID：** Microsoft.VisualStudio.Workload.DataScience

**描述：** 用于创建数据科学应用程序的语言和工具，包括 Python 和 F#。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 语言支持 | 16.4.29429.68 | 建议
Microsoft.Component.PythonTools.Minicondax64 | Python miniconda | 16.2.29003.222 | 建议
Microsoft.Component.PythonTools.Web | Python Web 支持 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 建议
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python 本机开发工具 | 16.2.29020.229 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.24) | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional

## <a name="net-desktop-development"></a>.NET 桌面开发

**ID：** Microsoft.VisualStudio.Workload.ManagedDesktop

**描述：** 通过 .NET Core 和 .NET Framework，使用 C#、Visual Basic 和 F# 生成 WPF、Windows 窗体和控制台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET 桌面开发工具 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 必需
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.1076 | 建议
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 16.0.28516.191 | 建议
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 LTS 运行时 | 16.4.29519.181 | 建议
Microsoft.NetCore.Component.DevelopmentTools | .NET Core 开发工具 | 16.4.29511.114 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 16.1.28811.260 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 建议
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 16.0.28528.71 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | Optional
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET framework 4.6.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 16.4.29318.151 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 16.0.28528.71 | Optional
Microsoft.VisualStudio.Component.CodeClone | 代码克隆 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | 实时依赖项验证 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | Optional
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | 体系结构和分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX 打包工具 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | Optional
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | Optional

## <a name="game-development-with-unity"></a>使用 Unity 的游戏开发

**ID：** Microsoft.VisualStudio.Workload.ManagedGame

**描述：** 使用 Unity（功能强大的跨平台开发环境）创建 2D 和 3D 游戏。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 开发工具 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.Unity | Visual Studio Tools for Unity | 16.0.28315.86 | 必需
Component.UnityEngine.x64 | Unity 2019.2（64 位）编辑器 | 16.4.29429.68 | 建议
Component.UnityEngine.x86 | Unity 5.6 32 位编辑器 | 16.1.28811.260 | 建议

## <a name="linux-development-with-c"></a>使用 C++ 的 Linux 开发

**ID：** Microsoft.VisualStudio.Workload.NativeCrossPlat

**描述：** 创建和调试在 Linux 环境中运行的应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.MDD.Linux | 适用于 Linux 开发的 C++ | 16.4.29511.114 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | 必需
Component.Linux.CMake | 适用于 Linux 的 C++ CMake 工具 | 16.2.29003.222 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 建议
Component.MDD.Linux.GCC.arm | 嵌入式和 IoT 开发工具 | 16.4.29429.68 | Optional

## <a name="desktop-development-with-c"></a>使用 C++ 的桌面开发

**ID：** Microsoft.VisualStudio.Workload.NativeDesktop

**描述：** 使用所选工具（包括 MSVC、Clang、CMake 或 MSBuild）生成适用于 Windows 的新式 C++ 应用。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 16.0.28528.71 | 必需
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 Redistributable 更新 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Native | 适用于 C++ 的体系结构工具 | 16.0.28621.142 | 必需
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | C++ 核心桌面功能 | 16.2.29012.281 | 必需
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.1076 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 建议
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer（实验性） | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.VC.ATL | 适用于最新 v142 生成工具的 C++ ATL（x86 和 x64） | 16.4.29313.120 | 建议
Microsoft.VisualStudio.Component.VC.CMake.Project | 用于 Windows 的 C++ CMake 工具 | 16.3.29103.31 | 建议
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Boost.Test 测试适配器 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Google Test 测试适配器 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.24) | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.CMake | JSON 编辑器 | 16.3.29207.166 | 建议
Component.Incredibuild | IncrediBuild - 生成加速 | 16.0.28528.71 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.10 | Optional
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 16.0.28625.61 | Optional
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ 生成工具 (v14.00) | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.ATLMFC | 适用于最新 v142 生成工具的 C++ MFC（x86 和 x64） | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.VC.CLI.Support | 适用于 v142 生成工具的 C++/CLI 支持 (14.24) | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.VC.Llvm.Clang | 适用于 Windows 的 C++ Clang 编译器 (9.0.0) | 16.4.29511.114 | Optional
Microsoft.VisualStudio.Component.VC.Llvm.ClangToolset | v142 生成工具的 C++ Clang-cl (x64/x86) | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | C++ Modules for v142 生成工具（x64/x86 - 试验） | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 生成工具 (v14.16) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang | 适用于 Windows 的 C++ Clang 工具 (9.0.0 - x64/x86) | 16.4.29511.114 | Optional

## <a name="game-development-with-c"></a>使用 C++ 的游戏开发

**ID：** Microsoft.VisualStudio.Workload.NativeGame

**描述：** 以 DirectX、Unreal 或 Cocos2d 为后盾，利用 C++ 的强大功能生成专业游戏。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 Redistributable 更新 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.24) | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer（实验性） | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | 建议
Component.Android.NDK.R16B | Android NDK (R16B) | 16.4.29519.181 | Optional
Component.Android.SDK25.Private | Android SDK 安装（API 级别 25）（使用 C++ 的移动开发的本地安装） | 16.0.28625.61 | Optional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Optional
Component.Cocos | Cocos | 16.0.28315.86 | Optional
Component.Incredibuild | IncrediBuild - 生成加速 | 16.0.28528.71 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.10 | Optional
Component.MDD.Android | C++ Android 开发工具 | 16.0.28517.75 | Optional
Component.OpenJDK | OpenJDK（Microsoft 分发） | 16.1.28811.260 | Optional
Component.Unreal | Unreal 引擎安装程序 | 16.1.28810.153 | Optional
Component.Unreal.Android | 适用于 Unreal 引擎的 Android IDE 支持 | 16.1.28810.153 | Optional
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 16.0.28516.191 | Optional
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional

## <a name="mobile-development-with-c"></a>使用 C++ 的移动开发

**ID：** Microsoft.VisualStudio.Workload.NativeMobile

**描述：** 使用 C++ 生成适用于 iOS、Android 或 Windows 的跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Android.SDK25.Private | Android SDK 安装（API 级别 25）（使用 C++ 的移动开发的本地安装） | 16.0.28625.61 | 必需
Component.OpenJDK | OpenJDK（Microsoft 分发） | 16.1.28811.260 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | 必需
Component.Android.NDK.R16B | Android NDK (R16B) | 16.4.29519.181 | 建议
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 建议
Component.MDD.Android | C++ Android 开发工具 | 16.0.28517.75 | 建议
Component.Android.NDK.R16B_3264 | Android NDK (R16B)（32 位） | 16.4.29519.181 | Optional
Component.Google.Android.Emulator.API25.Private | Google Android Emulator（API 级别 25）（本地安装） | 16.1.28810.153 | Optional
Component.HAXM.Private | Intel 硬件加速执行管理器 (HAXM)（本地安装） | 16.0.28528.71 | Optional
Component.Incredibuild | IncrediBuild - 生成加速 | 16.0.28528.71 | Optional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.10 | Optional
Component.MDD.IOS | C++ iOS 开发工具 | 16.0.28517.75 | Optional

## <a name="net-core-cross-platform-development"></a>.NET Core 跨平台开发

**ID：** Microsoft.VisualStudio.Workload.NetCoreTools

**描述：** 使用 .NET Core、ASP.NET Core、HTML/JavaScript 和包括 Docker 支持的容器生成跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | 必需
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.NetCore.Component.DevelopmentTools | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.NetCore.Component.Web | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 必需
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.1076 | 建议
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs 工具 | 16.0.28714.129 | 建议
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 LTS 运行时 | 16.4.29519.181 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 16.1.28810.153 | 建议
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 16.4.29313.120 | 建议
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Debugger.Snapshot | 快照调试程序 | 16.2.29003.222 | 建议
Microsoft.VisualStudio.Component.Debugger.TimeTravel | 按时间顺序查看调试器 | 16.4.29511.114 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 16.1.28811.260 | 建议
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs 工具 | 16.0.28621.142 | 建议
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | 用于 Web 开发的云工具 | 16.2.29003.222 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 开发时 IIS 支持 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX 打包工具 | 16.4.29409.204 | Optional

## <a name="mobile-development-with-net"></a>使用 .NET 的移动开发

**ID：** Microsoft.VisualStudio.Workload.NetCrossPlat

**描述：** 使用 Xamarin 生成适用于 iOS、Android 或 Windows 的跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.OpenJDK | OpenJDK（Microsoft 分发） | 16.1.28811.260 | 必需
Component.Xamarin | Xamarin | 16.4.29409.204 | 必需
Component.Xamarin.RemotedSimulator | Xamarin 远程模拟器 | 16.0.28315.86 | 必需
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.NetCore.Component.DevelopmentTools | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.Merq | 常见 Xamarin 内部工具 | 16.2.29012.281 | 必需
Microsoft.VisualStudio.Component.MonoDebugger | Mono 调试程序 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | ASP.NET 模板化引擎 | 16.0.28315.86 | 必需
Component.Android.SDK28 | Android SDK 安装程序（API 级别 28） | 16.2.29003.222 | 建议

## <a name="aspnet-and-web-development"></a>ASP.NET 和 Web 开发

**ID：** Microsoft.VisualStudio.Workload.NetWeb

**描述：** 使用 ASP.NET Core、ASP.NET、HTML/JavaScript 和包括 Docker 支持的容器生成 Web 应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | 必需
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.NetCore.Component.DevelopmentTools | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.NetCore.Component.Web | .NET Core 开发工具 | 16.4.29511.114 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 必需
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.1076 | 建议
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs 工具 | 16.0.28714.129 | 建议
Microsoft.Net.Component.4.5.1.TargetingPack | .NET Framework 4.5.1 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 16.0.28517.75 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4 – 4.6 开发工具 | 16.0.28516.191 | 建议
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 LTS 运行时 | 16.4.29519.181 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.AspNet45 | 高级 ASP.NET 功能 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 16.1.28810.153 | 建议
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 16.4.29313.120 | 建议
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | 建议
Microsoft.VisualStudio.Component.Debugger.Snapshot | 快照调试程序 | 16.2.29003.222 | 建议
Microsoft.VisualStudio.Component.Debugger.TimeTravel | 按时间顺序查看调试器 | 16.4.29511.114 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 16.0.28315.86 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 16.1.28811.260 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs 工具 | 16.0.28621.142 | 建议
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | 用于 Web 开发的云工具 | 16.2.29003.222 | 建议
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET framework 4.6.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 16.4.29318.151 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 16.0.28528.71 | Optional
Microsoft.VisualStudio.Component.CodeClone | 代码克隆 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | 实时依赖项验证 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.TestTools.WebLoadTest | Web 性能和负载测试工具 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Optional
Microsoft.VisualStudio.ComponentGroup.AdditionalWebProjectTemplates | 其他项目模板（早期版本） | 16.0.28621.142 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | 体系结构和分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 开发时 IIS 支持 | 16.0.28315.86 | Optional

## <a name="nodejs-development"></a>Node.js 开发

**ID：** Microsoft.VisualStudio.Workload.Node

**描述：** 使用 Node.js（一个由异步事件驱动的 JavaScript 运行时）生成可缩放的网络应用程序。 

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.Node.Tools | Node.js 开发工具 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 必需
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.1076 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.24) | 16.4.29409.204 | Optional

## <a name="officesharepoint-development"></a>Office/SharePoint 开发

**ID：** Microsoft.VisualStudio.Workload.Office

**描述：** 使用 C#、VB 和 JavaScript 创建 Office 和 SharePoint 外接程序、SharePoint 解决方案和 VSTO 外接程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | 必需
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.Component.4.TargetingPack | .NET Framework 4 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET 桌面开发工具 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.Sharepoint.Tools | Visual Studio 的 Office 开发工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 必需
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 16.0.28315.86 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 必需
Microsoft.VisualStudio.Component.TeamOffice | Visual Studio Tools for Office (VSTO) | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | .NET framework 4.6.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | .NET Framework 4.6.2 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | .NET Framework 4.7.1 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | .NET Framework 4.7 开发工具 | 16.3.29207.166 | Optional
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 16.4.29318.151 | Optional
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | Optional
Microsoft.VisualStudio.ComponentGroup.Sharepoint.WIF | Windows Identity Foundation 3.5 | 16.0.28621.142 | Optional

## <a name="python-development"></a>Python 开发

**ID：** Microsoft.VisualStudio.Workload.Python

**描述：** 对 Python 进行编辑、调试、交互式开发和源代码管理。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 语言支持 | 16.4.29429.68 | 必需
Component.CPython3.x64 | Python 3（64 位）(3.7.5) | 3.7.5 | 建议
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.1076 | 建议
Microsoft.Component.PythonTools.Minicondax64 | Python miniconda | 16.2.29003.222 | 建议
Microsoft.Component.PythonTools.Web | Python Web 支持 | 16.0.28517.75 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 16.4.29409.204 | 建议
Microsoft.VisualStudio.Component.TypeScript.3.7 | TypeScript 3.7 SDK | 16.0.29429.68 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 16.0.28517.75 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 16.0.28621.142 | 建议
Component.CPython2.x64 | Python 2（64 位）(2.7.16) | 2.7.16 | Optional
Component.CPython2.x86 | Python 2（32 位）(2.7.16) | 2.7.16 | Optional
Component.CPython3.x86 | Python 3（32 位）(3.7.5) | 3.7.5 | Optional
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 16.0.28714.129 | Optional
Component.Microsoft.Web.LibraryManager | 库管理器 | 16.0.28315.86 | Optional
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | Optional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python 本机开发工具 | 16.2.29020.229 | Optional
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | Optional
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | Optional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 16.1.28810.153 | Optional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Azure 存储仿真程序 | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 16.4.29318.151 | Optional
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 16.0.28707.177 | Optional
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | Optional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.SQL.ADAL | SQL ADAL 运行时 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 16.0.28315.86 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.24) | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发工具 | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发工具先决条件 | 16.4.29318.151 | Optional

## <a name="universal-windows-platform-development"></a>通用 Windows 平台开发

**ID：** Microsoft.VisualStudio.Workload.Universal

**描述：** 使用 C#、VB、或可选 C++ 为通用 Windows 平台创建应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.NetFX.Native | .NET Native | 16.4.29429.68 | 必需
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | 必需
Microsoft.Net.Component.4.5.TargetingPack | .NET Framework 4.5 目标包 | 16.0.28517.75 | 必需
Microsoft.NetCore.Component.SDK | .NET Core 3.1 SDK | 16.4.29519.181 | 必需
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.Graphics | 图像和 3D 模型编辑器 | 16.0.28517.75 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 16.0.28315.86 | 必需
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 16.1.28829.92 | 必需
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX 打包工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET 本机和 .NET 标准 | 16.3.29102.218 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.Support | 通用 Windows 平台工具 | 16.4.29409.204 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | 适用于 Xamarin 的通用 Windows 平台工具 | 16.4.29511.114 | 必需
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | Optional
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | Optional
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 16.0.28528.71 | Optional
Microsoft.VisualStudio.Component.CodeClone | 代码克隆 | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | 实时依赖项验证 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | 用于 v142 生成工具的 C++ 通用 Windows 平台支持 (ARM64) | 16.3.29207.166 | Optional
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 16.0.28625.61 | Optional
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2019 Redistributable 更新 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM | MSVC v142 - VS 2019 C++ ARM 生成工具 (v14.24) | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v142 - VS 2019 C++ ARM64 生成工具 (v14.24) | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.24) | 16.4.29409.204 | Optional
Microsoft.VisualStudio.Component.VC.v141.ARM | MSVC v141 – VS 2017 C++ ARM 生成工具 (v14.16) | 16.2.29003.222 | Optional
Microsoft.VisualStudio.Component.VC.v141.ARM64 | MSVC v141 – VS 2017 C++ ARM64 生成工具 (v14.16) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 生成工具 (v14.16) | 16.1.28829.92 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | Windows 10 SDK (10.0.16299.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | Windows 10 SDK (10.0.17134.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | Windows 10 SDK (10.0.17763.0) | 16.0.28517.75 | Optional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | USB 设备连接性 | 16.4.29511.114 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | 体系结构和分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Native | 适用于 C++ 的体系结构工具 | 16.0.28621.142 | Optional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | C++ 核心桌面功能 | 16.2.29012.281 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ (v142) 通用 Windows 平台工具 | 16.3.29207.166 | Optional
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v141 | C++ (v141) 通用 Windows 平台工具 | 16.1.28810.153 | Optional

## <a name="visual-studio-extension-development"></a>Visual Studio 扩展开发

**ID：** Microsoft.VisualStudio.Workload.VisualStudioExtension

**描述：** 为 Visual Studio 创建加载项和扩展，包括新命令、代码分析器和工具窗口。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | name | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.4.29429.68 | 必需
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 16.0.28517.75 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 16.4.29313.120 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 16.3.29207.166 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 0.1 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 16.1.28829.92 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 16.0.28714.129 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 16.4.29429.68 | 必需
Microsoft.VisualStudio.Component.VSSDK | Visual Studio SDK | 16.0.28315.86 | 必需
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Visual Studio 扩展开发必备组件 | 16.4.29318.151 | 必需
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.4.29429.68 | 建议
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 16.0.28625.61 | 建议
Microsoft.Component.CodeAnalysis.SDK | .NET 编译器平台 SDK | 16.2.29003.222 | Optional
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 16.4.29429.68 | Optional
Microsoft.VisualStudio.Component.DslTools | 建模 SDK | 16.0.28315.86 | Optional

## <a name="unaffiliated-components"></a>独立组件

这些组件不随附于任何工作负载，但可选择作为单个组件。

组件 ID | name | Version
--- | --- | ---
Component.GitHub.VisualStudio | 适用于 Visual Studio 的 GitHub 扩展 | 2.5.9.5485
Component.Xamarin.Inspector | Xamarin Inspector | 16.0.28315.86
Component.Xamarin.Profiler | Xamarin Profiler | 16.0.28315.86
Component.Xamarin.Workbooks | Xamarin Workbooks | 16.0.28315.86
Microsoft.Component.ClickOnce | ClickOnce 发布 | 16.4.29409.204
Microsoft.Component.HelpViewer | 帮助查看器 | 16.0.28625.61
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 16.4.29409.204
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 16.4.29409.204
Microsoft.Net.Core.Component.SDK.2.2 | .NET Core 2.2 运行时 | 16.4.29519.181
Microsoft.Net.Core.Component.SDK.3.0 | .NET Core 3.0 运行时 | 16.4.29519.181
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | 开发工具和 .NET Core 2.1 | 16.3.29207.166
Microsoft.NetCore.ComponentGroup.Web.2.1 | Web 开发工具和 .NET Core 2.1 | 16.3.29207.166
Microsoft.VisualStudio.Component.AzureDevOps.OfficeIntegration | Azure DevOps Office 集成 | 16.0.28625.61
Microsoft.VisualStudio.Component.Debugger.VSOnline | 用于 Visual Studio Online 环境的调试程序 | 16.4.29429.68
Microsoft.VisualStudio.Component.Git | 用于 Windows 的 Git | 16.0.28625.61
Microsoft.VisualStudio.Component.LinqToSql | LINQ to SQL 工具 | 16.0.28625.61
Microsoft.VisualStudio.Component.TestTools.CodedUITest | 编码的 UI 测试 | 16.0.28327.66
Microsoft.VisualStudio.Component.VC.14.20.ARM | MSVC v142 – VS 2019 C++ ARM 生成工具 (v14.20) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ARM.Spectre | MSVC v142 – VS 2019 C++ ARM Spectre 缓解库 (v14.20) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ARM64 | MSVC v142 – VS 2019 C++ ARM64 生成工具 (v14.20) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ARM64.Spectre | MSVC v142 – VS 2019 C++ ARM64 Spectre 缓解库 (v14.20) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ATL | v142 生成工具的 C++ v14.20 ATL（x86 和 x64） | 16.1.28829.92
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM | v142 生成工具的 C++ v14.20 ATL (ARM) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.20 ATL (ARM) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM64 | v142 生成工具的 C++ v14.20 ATL (ARM64) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的 用于 v142 生成工具的 C++ v14.20 ATL (ARM64) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.ATL.Spectre | 带有 Spectre 缓解措施的 用于 v142 生成工具的 C++ v14.20 ATL（x86 和 x64） | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.CLI.Support | v142 生成工具的 C++/CLI 支持 (14.20) | 16.4.29409.204
Microsoft.VisualStudio.Component.VC.14.20.MFC | v142 生成工具的 C++ v14.20 MFC（x86 和 x64） | 16.2.29003.222
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM | v142 生成工具的 C++ v14.20 MFC (ARM) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.20 MFC (ARM) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM64 | v142 生成工具的 C++ v14.20 MFC (ARM64) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的 用于 v142 生成工具的 C++ v14.20 MFC (ARM64) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.MFC.Spectre | 带有 Spectre 缓解措施的 用于 v142 生成工具的 C++ v14.20 MFC（x86 和 x64） | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.x86.x64 | MSVC v142 – VS 2019 C++ x64/x86 生成工具 (v14.20) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.20.x86.x64.Spectre | MSVC v142 – VS 2019 C++ x64/x86 Spectre 缓解库 (v14.20) | 16.4.29511.114
Microsoft.VisualStudio.Component.VC.14.21.ARM | MSVC v142 – VS 2019 C++ ARM 生成工具 (v14.21) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.14.21.ARM.Spectre | MSVC v142 – VS 2019 C++ ARM Spectre 缓解库 (v14.21) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.ARM64 | MSVC v142 – VS 2019 C++ ARM64 生成工具 (v14.21) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.14.21.ARM64.Spectre | MSVC v142 – VS 2019 C++ ARM64 Spectre 缓解库 (v14.21) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.ATL | v142 生成工具的 C++ v14.21 ATL（x86 和 x64） | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM | v142 生成工具的 C++ v14.21 ATL (ARM) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.21 ATL (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM64 | v142 生成工具的 C++ v14.21 ATL (ARM64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM64.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.21 ATL (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.ATL.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.21 ATL（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.CLI.Support | v142 生成工具的 C++/CLI 支持 (14.21) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.14.21.MFC | v142 生成工具的 C++ v14.21 MFC（x86 和 x64） | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM | v142 生成工具的 C++ v14.21 MFC (ARM) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.21 MFC (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM64 | v142 生成工具的 C++ v14.21 MFC (ARM64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM64.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.21 MFC (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.MFC.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.21 MFC（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.21.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.21) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.14.21.x86.x64.Spectre | MSVC v142 – VS 2019 C++ x64/x86 Spectre 缓解库 (v14.21) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.ARM | MSVC v142 - VS 2019 C++ ARM 生成工具 (v14.22) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 缓解库 (v14.22) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.ARM64 | MSVC v142 - VS 2019 C++ ARM64 生成工具 (v14.22) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 缓解库 (v14.22) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.ATL | 适用于 v142 生成工具的 C++ v14.22 ATL（x86 和 x64） | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM | 适用于 v142 生成工具的 C++ v14.22 ATL (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM.Spectre | 带有 Spectre 缓解措施的 v142 生成工具的 C++ v14.22 (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM64 | 适用于 v142 生成工具的 C++ v14.22 ATL (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.22 ATL (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.ATL.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.22 ATL（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.CLI.Support | v142 生成工具的 C++/CLI 支持 (14.22) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC | 适用于 v142 生成工具的 C++ v14.22 MFC（x86 和 x64） | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM | 适用于 v142 生成工具的 C++ v14.22 MFC (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.22 MFC (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM64 | 适用于 v142 生成工具的 C++ v14.22 MFC (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.22 MFC (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.MFC.Spectre | 带有 Spectre 缓解措施的 v142 生成工具的 C++ v14.22 MFC（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.22.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.22) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.14.22.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 缓解库 (v14.22) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ARM | MSVC v142 - VS 2019 C++ ARM 生成工具 (v14.23) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 缓解库 (v14.23) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ARM64 | MSVC v142 - VS 2019 C++ ARM64 生成工具 (v14.23) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 缓解库 (v14.23) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ATL | 适用于 v142 生成工具的 C++ v14.23 ATL（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM | 适用于 v142 生成工具的 C++ v14.23 ATL (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM.Spectre | 带有 Spectre 缓解库的 v142 生成工具的 C++ v14.23 ATL (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM64 | 适用于 v142 生成工具的 C++ v14.23 ATL (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.23 ATL (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.ATL.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.23 ATL（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.CLI.Support | 适用于 v142 生成工具的 C++/CLI 支持 (14.23) | 16.4.29409.204
Microsoft.VisualStudio.Component.VC.14.23.MFC | 适用于 v142 生成工具的 C++ v14.23 MFC（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM | 适用于 v142 生成工具的 C++ v14.23 MFC (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.23 MFC (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM64 | 适用于 v142 生成工具的 C++ v14.23 MFC (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的用于 v142 生成工具的 C++ v14.23 MFC (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.MFC.Spectre | 带有 Spectre 缓解措施的 v142 生成工具的 C++ v14.23 MFC（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.23) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.14.23.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 缓解库 (v14.23) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.ATL.ARM | 适用于最新 v142 生成工具的 C++ ATL (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | 带有 Spectre 缓解措施的适用于最新的 v142 生成工具的 C++ ATL (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | 适用于最新 v142 生成工具的 C++ ATL (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的适用于最新的 v142 生成工具的 C++ ATL (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.ATL.Spectre | 带有 Spectre 缓解措施的适用于最新 v142 生成工具的 C++ ATL（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | 带有 Spectre 缓解措施的适用于最新的 v142 生成工具的 C++ MFC（x86 和 x64） | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.MFC.ARM | 适用于最新 v142 生成工具的 C++ MFC (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | 带有 Spectre 缓解措施的适用于最新 v142 生成工具的 C++ MFC (ARM) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | 适用于最新 v142 生成工具的 C++ MFC (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的适用于最新 v142 生成工具的 C++ MFC (ARM64) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.Redist.MSM | C++ 2019 Redistributable MSM | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 缓解库 (v14.24) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 缓解库 (v14.24) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 缓解库 (v14.24)  | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.v141.ARM.Spectre | MSVC v141 – VS 2017 C++ ARM Spectre 缓解库 (v14.16) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.v141.ARM64.Spectre | MSVC v141 – VS 2017 C++ ARM64 Spectre 缓解库 (v14.16) | 16.4.29429.68
Microsoft.VisualStudio.Component.VC.v141.ATL | C++ ATL for v141 生成工具 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM | C++ ATL for v141 生成工具 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM.Spectre | 带有 Spectre 缓解措施的 C++ ATL for v141 生成工具 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64 | C++ ATL for v141 生成工具 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的 C++ ATL for v141 生成工具 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.Spectre | 带有 Spectre 缓解措施的 C++ ATL for v141 生成工具（x86 和 x64） | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.CLI.Support | v141 生成工具的 C++/CLI 支持 (14.16) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.v141.MFC | C++ MFC for v141 生成工具（x86 和 x64） | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM | C++ MFC for v141 生成工具 (ARM) | 16.2.28915.88
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM.Spectre | 带有 Spectre 缓解措施的 C++ MFC for v141 生成工具 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64 | C++ MFC for v141 生成工具 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的 C++ MFC for v141 生成工具 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.Spectre | 带有 Spectre 缓解措施的 C++ MFC for v141 生成工具 (x86 & x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.x86.x64.Spectre | MSVC v141 – VS 2017 C++ x64/x86 Spectre 缓解库 (v14.16) | 16.4.29429.68
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 16.0.28707.177
Microsoft.VisualStudio.Component.WinXP | VS 2017 (v141) 工具的 C++ Windows XP 支持 [已弃用] | 16.1.28811.260
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 16.1.28810.153
