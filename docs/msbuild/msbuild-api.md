---
title: MSBuild API | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9d3cdaf2bcc7d7c62f7224c3a8c439d03282ef0
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371919"
---
# <a name="use-the-msbuild-api"></a>使用 MSBuild API

MSBuild 提供公共 API 外围，因此程序可以执行生成操作和检查项目。 可在以下 NuGet 包中找到最新版的 MSBuild API：

| 包名称 | 描述 |
| ------------ | ----------- |
| [Microsoft.Build](https://www.nuget.org/packages/Microsoft.Build) | 包含用于创建、编辑和评估 MSBuild 项目的 Microsoft.Build 程序集。|
| [Microsoft.Build.Framework](https://www.nuget.org/packages/Microsoft.Build.Framework)| 包含其他 MSBuild 程序集所用的通用 MSBuild 框架程序集。 |
| [Microsoft.Build.Runtime](https://www.nuget.org/packages/Microsoft.Build.Runtime) | 提供 MSBuild 的完整可执行文件副本。 仅当应用程序需要在无需安装 MSBuild 的情况下加载项目或执行进程内生成操作时，才引用此包。 若要使用此包成功地评估项目，需要将其他组件（如编译器）聚合到应用程序目录。 |
| [Microsoft.Build.Tasks.Core](https://www.nuget.org/packages/Microsoft.Build.Tasks.Core) | 包含可实现 MSBuild 的常用任务的 Microsoft.Build.Tasks 程序集。 |
| [Microsoft.Build.Utilities.Core](https://www.nuget.org/packages/Microsoft.Build.Utilities.Core) | 包含用于实现自定义 MSBuild 任务的 Microsoft.Build.Utilities 程序集。 |

此外，NuGet 还托管了一个已弃用的旧版程序集 [Microsoft.Build.Engine](https://www.nuget.org/packages/Microsoft.Build.Engine)。

MSBuild API 有几种不同版本，对于版本 15 和 16，NuGet 包中有两种不同形式的程序集，一种使用 .NET Framework 进行编译，另一种使用 .NET Core 进行编译，同时也是 .NET Framework API 图面的子集。  调用 `dotnet` 命令以及在 Mac 和 Linux 系统上使用 MSBuild 时，将使用 .NET Core 版的 MSBuild。

可以通过使用 [.NET API 浏览器](/dotnet/api)或浏览下表中的命名空间查找 MSBuild API 的文档。

::: moniker range="vs-2017"
| 命名空间 | 适用于 | 描述 |
|-----------| -----------| ----------- |
| [Microsoft.Build.Construction](/dotnet/api/Microsoft.Build.Construction?view=msbuild-15) | 全部 |  包含 MSBuild 对象模型用于构造具有未评估值的项目根的类型。 每个项目根都对应一个项目或目标文件。 |
| [Microsoft.Build.Definition](/dotnet/api/Microsoft.Build.Definition?view=msbuild-15) | 全部 | 包含支持项目构造的 `ProjectOptions` 类。 |
| [Microsoft.Build.Evaluation](/dotnet/api/Microsoft.Build.Evaluation?view=msbuild-15) | 全部 | 包含 MSBuild 对象模型用于评估项目的类型。 每个项目都与一个或多个项目根相关联。 |
| [Microsoft.Build.Evaluation.Context](/dotnet/api/Microsoft.Build.Evaluation.Context?view=msbuild-15) | 全部 | 包含 `EvaluationContext` 类，用于存储各个调用的评估状态。 |
| [Microsoft.Build.Exceptions](/dotnet/api/Microsoft.Build.Exceptions?view=msbuild-15) | 全部 | 包含可能在生成过程中引发的异常类型。 |
| [Microsoft.Build.Execution](/dotnet/api/Microsoft.Build.Execution?view=msbuild-15) | 全部 | 包含 MSBuild 对象模型用于生成项目的类型。 |
| [Microsoft.Build.Framework](/dotnet/api/Microsoft.Build.Framework?view=msbuild-15) | 全部 | 包含定义任务和记录器与 MSBuild 引擎的交互方式的类型。|
| [Microsoft.Build.Framework.Profiler](/dotnet/api/Microsoft.Build.Framework.Profiler?view=msbuild-15) | 全部 | 包含支持性能分析的类型。 |
| [Microsoft.Build.Framework.XamlTypes](/dotnet/api/Microsoft.Build.Framework.XamlTypes?view=msbuild-15) | 仅限 .NET Framework | 包含用于表示根据文件、规则和其他源分析的 XAML 类型的类。 |
| [Microsoft.Build.Globbing](/dotnet/api/Microsoft.Build.Globbing?view=msbuild-15) | 全部 | 包含支持通配符处理的类。 |
| [Microsoft.Build.Globbing.Extensions](/dotnet/api/Microsoft.Build.Globbing.Extensions?view=msbuild-15) | 全部 | 包含支持通配符处理扩展的类型。 |
| [Microsoft.Build.Graph](/dotnet/api/Microsoft.Build.Graph?view=msbuild-15) | 全部 | 包含支持 `-graph` MSBuild 开关的类型。 |
| [Microsoft.Build.Logging](/dotnet/api/Microsoft.Build.Logging?view=msbuild-15) | 全部 | 包含用于记录生成进度的类型。 |
| [Microsoft.Build.ObjectModelRemoting](/dotnet/api/Microsoft.Build.ObjectModelRemoting?view=msbuild-15) | 全部 | 包含支持 MSBuild 中的远程处理的类型。 |
| [Microsoft.Build.Tasks](/dotnet/api/Microsoft.Build.Tasks?view=msbuild-15) | 全部 | 包含 MSBuild 附带的所有任务的实现。 |
| [Microsoft.Build.Tasks.Deployment.Bootstrapper](/dotnet/api/Microsoft.Build.Tasks.Deployment.Bootstrapper?view=msbuild-15) | 仅限 .NET Framework | 包含 MSBuild 在内部使用的类。 |
| [Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/Microsoft.Build.Tasks.Deployment.ManifestUtilities?view=msbuild-15) | 仅限 .NET Framework | 包含 MSBuild 使用的类。|
| [Microsoft.Build.Tasks.Hosting](/dotnet/api/Microsoft.Build.Tasks.Hosting?view=msbuild-15) | 全部 | 包含 MSBuild 在内部使用的类。 |
| [Microsoft.Build.Tasks.Xaml](/dotnet/api/Microsoft.Build.Tasks.Xaml?view=msbuild-15) | 仅限 .NET Framework | 包含与 XAML 生成任务相关的类。 |
| [Microsoft.Build.Utilities](/dotnet/api/Microsoft.Build.Utilities?view=msbuild-15) | 全部 | 包含可用于创建你自己的 MSBuild 记录器和任务的帮助程序类。|
:::moniker-end
:::moniker range=">=vs-2019"
| 命名空间 | 适用于 | 描述 |
|-----------| -----------| ----------- |
| [Microsoft.Build.Construction](/dotnet/api/Microsoft.Build.Construction?view=msbuild-16) | 全部 |  包含 MSBuild 对象模型用于构造具有未评估值的项目根的类型。 每个项目根都对应一个项目或目标文件。 |
| [Microsoft.Build.Definition](/dotnet/api/Microsoft.Build.Definition?view=msbuild-16) | 全部 | 包含支持项目构造的 `ProjectOptions` 类。 |
| [Microsoft.Build.Evaluation](/dotnet/api/Microsoft.Build.Evaluation?view=msbuild-16) | 全部 | 包含 MSBuild 对象模型用于评估项目的类型。 每个项目都与一个或多个项目根相关联。 |
| [Microsoft.Build.Evaluation.Context](/dotnet/api/Microsoft.Build.Evaluation.Context?view=msbuild-16) | 全部 | 包含 `EvaluationContext` 类，用于存储各个调用的评估状态。 |
| [Microsoft.Build.Exceptions](/dotnet/api/Microsoft.Build.Exceptions?view=msbuild-16) | 全部 | 包含可能在生成过程中引发的异常类型。 |
| [Microsoft.Build.Execution](/dotnet/api/Microsoft.Build.Execution?view=msbuild-16) | 全部 | 包含 MSBuild 对象模型用于生成项目的类型。 |
| [Microsoft.Build.Framework](/dotnet/api/Microsoft.Build.Framework?view=msbuild-16) | 全部 | 包含定义任务和记录器与 MSBuild 引擎的交互方式的类型。|
| [Microsoft.Build.Framework.Profiler](/dotnet/api/Microsoft.Build.Framework.Profiler?view=msbuild-16) | 全部 | 包含支持性能分析的类型。 |
| [Microsoft.Build.Framework.XamlTypes](/dotnet/api/Microsoft.Build.Framework.XamlTypes?view=msbuild-16) | 仅限 .NET Framework | 包含用于表示根据文件、规则和其他源分析的 XAML 类型的类。 |
| [Microsoft.Build.Globbing](/dotnet/api/Microsoft.Build.Globbing?view=msbuild-16) | 全部 | 包含支持通配符处理的类。 |
| [Microsoft.Build.Globbing.Extensions](/dotnet/api/Microsoft.Build.Globbing.Extensions?view=msbuild-16) | 全部 | 包含支持通配符处理扩展的类型。 |
| [Microsoft.Build.Graph](/dotnet/api/Microsoft.Build.Graph?view=msbuild-16) | 全部 | 包含支持 `-graph` MSBuild 开关的类型。 |
| [Microsoft.Build.Logging](/dotnet/api/Microsoft.Build.Logging?view=msbuild-16) | 全部 | 包含用于记录生成进度的类型。 |
| [Microsoft.Build.ObjectModelRemoting](/dotnet/api/Microsoft.Build.ObjectModelRemoting?view=msbuild-16) | 全部 | 包含支持 MSBuild 中的远程处理的类型。 |
| [Microsoft.Build.Tasks](/dotnet/api/Microsoft.Build.Tasks?view=msbuild-16) | 全部 | 包含 MSBuild 附带的所有任务的实现。 |
| [Microsoft.Build.Tasks.Deployment.Bootstrapper](/dotnet/api/Microsoft.Build.Tasks.Deployment.Bootstrapper?view=msbuild-16) | 仅限 .NET Framework | 包含 MSBuild 在内部使用的类。 |
| [Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/Microsoft.Build.Tasks.Deployment.ManifestUtilities?view=msbuild-16) | 仅限 .NET Framework | 包含 MSBuild 使用的类。|
| [Microsoft.Build.Tasks.Hosting](/dotnet/api/Microsoft.Build.Tasks.Hosting?view=msbuild-16) | 全部 | 包含 MSBuild 在内部使用的类。 |
| [Microsoft.Build.Tasks.Xaml](/dotnet/api/Microsoft.Build.Tasks.Xaml?view=msbuild-16) | 仅限 .NET Framework | 包含与 XAML 生成任务相关的类。 |
| [Microsoft.Build.Utilities](/dotnet/api/Microsoft.Build.Utilities?view=msbuild-16) | 全部 | 包含可用于创建你自己的 MSBuild 记录器和任务的帮助程序类。|
:::moniker-end

在上表中，“适用对象”列中的“所有”表示命名空间中的类型在 .NET Framework 版和 .NET Core 版的 MSBuild API 中可用。
