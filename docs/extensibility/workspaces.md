---
title: Visual Studio 中的工作区 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 011781b434c4d005e473c5f97c60a9269dc5d034
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952758"
---
# <a name="workspaces"></a>工作区

工作区是指 Visual Studio 如何表示 [打开的文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)中的任何文件集合，并由类型表示 <xref:Microsoft.VisualStudio.Workspace.IWorkspace> 。 工作区本身并不了解与文件夹中的文件相关的内容或功能。 相反，它提供了一组通用的 Api，用于生成和使用其他人可操作的数据。 使用各种导出属性，可通过 [Managed Extensibility Framework](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (MEF) 编写生成方。

## <a name="workspace-providers-and-services"></a>工作区提供程序和服务

工作区提供程序和服务提供数据和功能来响应工作区的内容。 它们可能会提供上下文文件信息、源文件中的符号或生成功能。

这两个概念都使用 [工厂模式](https://en.wikipedia.org/wiki/Factory_method_pattern) ，并通过工作区通过 MEF 导入。 所有导出特性 `IProviderMetadataBase` 都实现或 `IWorkspaceServiceFactoryMetadata` ，但是，扩展应将这些具体类型用于导出类型。

提供程序和服务之间的一个差异是它们与工作区之间的关系。 工作区可以有多个特定类型的提供程序，但每个工作区只创建一个特定类型的服务。 例如，工作区包含多个文件扫描程序提供程序，但工作区每个工作区只有一个索引服务。

另一个主要区别是提供程序和服务的数据消耗。 工作区是从提供程序获取数据的入口点，原因有几个。 首先，提供程序通常会创建一些较窄的数据集。 数据可以是 c # 源文件的符号，也可以是 _CMakeLists.txt_ 文件的生成文件上下文。 工作区会将使用者的请求匹配到元数据与请求对齐的提供程序。 其次，某些方案允许多个提供程序参与请求，而其他方案则使用具有最高优先级的访问接口。

与此相反，扩展可以获取实例，并直接与工作区服务交互。 上的扩展方法 `IWorkspace` 可用于 Visual Studio 提供的服务，例如 <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> 。 扩展可以为扩展中的组件或其他要使用的扩展提供工作区服务。 使用者应使用 <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetServiceAsync%2A> 或你在类型上提供的扩展方法 `IWorkspace` 。

>[!WARNING]
> 不要创作与 Visual Studio 冲突的服务。 这可能会导致意外的问题。

## <a name="disposal-on-workspace-closure"></a>工作区闭包处理

工作区结束时，扩展程序可能需要释放但调用异步代码。 <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable>此接口可用于轻松编写此代码。

## <a name="related-types"></a>相关类型

- <xref:Microsoft.VisualStudio.Workspace.IWorkspace> 打开的工作区（如打开的文件夹）的中心实体。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceProviderFactory`1> 创建每个工作区实例化的提供程序。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceServiceFactory> 创建每个工作区的服务实例化。
- <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable> 应对需要在处理过程中运行异步代码的提供程序和服务实现。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper> 提供用于访问已知服务或任意服务的帮助器方法。

## <a name="workspace-settings"></a>工作区设置

工作区具有对 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> 工作区具有简单但功能强大的控制的服务。 有关设置的基本概述，请参阅 [自定义生成和调试任务](../ide/customize-build-and-debug-tasks-in-visual-studio.md)。

大多数类型的设置 `SettingsType` 都是 _json_ 文件，例如 _VSWorkspaceSettings.js上_ 的和 _tasks.vs.js_。

工作区设置的功能围绕 "范围"，这只是工作区中的路径。 当使用者调用时 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> ，将聚合包含请求的路径和设置类型的所有范围。 范围聚合优先级如下：

1. "本地设置"，通常是工作区根目录的 `.vs` 目录。
1. 请求的路径本身。
1. 请求的路径的父目录。
1. 所有进一步的父目录，包括工作区根。
1. 用户目录中的 "全局设置"。

结果为的实例 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> 。 此对象保存特定类型的设置，并可查询设置存储为的密钥名称 `string` 。 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings.GetProperty%2A>方法和 <xref:Microsoft.VisualStudio.Workspace.Settings.WorkspaceSettingsExtensions> 扩展方法预期调用方知道所请求的设置值的类型。 由于大多数设置文件都作为 _json_ 文件保存，因此许多调用将使用 `string` 、 `bool` 、 `int` 和这些类型的数组。 还支持对象类型。 在这些情况下，可以将 `IWorkspaceSettings` 自身用作类型参数。 例如：

```json
{
  "intValue": 1,
  "stringValue": "s",
  "boolValue": true,
  "stringArray": [
    "s1",
    "s2"
  ],
  "nestedIWorkspaceSettings": {
    "nestedString": "ns"
  }
}
```

假设这些设置位于用户 _VSWorkspaceSettings.js上_的，则可以访问数据，如下所示：

```csharp
using System.Collections.Generic;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static void ReadSettings(IWorkspace workspace)
{
    IWorkspaceSettingsManager settingsManager = workspace.GetSettingsManager();
    IWorkspaceSettings settings = settingsManager.GetAggregatedSettings(SettingsTypes.Generic);

    // result == WorkspaceSettingsResult.Success
    WorkspaceSettingsResult result = settings.GetProperty("intValue", out int intValue);
    result = settings.GetProperty("stringValue", out string stringValue);
    result = settings.GetProperty("boolValue", out bool boolValue);
    result = settings.GetProperty("stringArray", out string[] stringArray);
    result = settings.GetProperty("nestedIWorkspaceSettings", out IWorkspaceSettings nestedIWorkspaceSettings);
    result = nestedIWorkspaceSettings.GetProperty("nestedString", out string nestedString);

    // Extension method alternative using default values.
    int intValueOrDefault = settings.Property("intValue", /* default */ 42);

    // Missing key. result == WorkspaceSettingsResult.Undefined
    result = settings.GetProperty("missing", out string missing);

    // Wrong type for a key. result == WorkspaceSettingsResult.Error
    result = settings.GetProperty("intValue", out IWorkspaceSettings notSettings);

    // Special ability to union "stringArray" across all scopes.
    IEnumerable<string> allStringArray = settings.UnionPropertyArray<string>("stringArray");
}
```

>[!NOTE]
>这些设置 Api 与命名空间中提供的 Api 无关 `Microsoft.VisualStudio.Settings` 。 工作区设置与主机无关，并使用特定于工作区的设置文件或动态设置提供程序。

### <a name="providing-dynamic-settings"></a>提供动态设置

扩展可以提供 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProvider> 。 这些内存中提供程序允许扩展添加设置或覆盖其他设置。

导出与 `IWorkspaceSettingsProvider` 其他工作区提供程序不同。 工厂不是 `IWorkspaceProviderFactory` ，并且没有特殊的属性类型。 而是实现 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProviderFactory> 和使用 `[Export(typeof(IWorkspaceSettingsProviderFactory))]` 。

```csharp
// Common workspace provider factory pattern
[ExportFeatureProvider(some, args, to, export)]
internal class MyProviderFactory : IWorkspaceProviderFactory<IFeatureProvider>
{
     IFeatureProvider CreateProvider(IWorkspace workspace) => new Provider(workspace);
}

// IWorkspaceSettingsProvider pattern
[Export(typeof(IWorkspaceSettingsProviderFactory))]
internal class MySettingsProviderFactory : IWorkspaceSettingsProviderFactory
{
    // 100 is typically the value used by built-in settings providers. Lower value is higher priority.
    int Priority => 100;

    IWorkspaceSettingsProvider CreateSettingsProvider(IWorkspace workspace) => new MySettingsProvider(workspace);
}
```

>[!TIP]
>实现返回 `IWorkspaceSettingsSource` (如) 的方法时 `IWorkspaceSettingsProvider.GetSingleSettings` ，将返回的实例， `IWorkspaceSettings` 而不是 `IWorkspaceSettingsSource` 。 `IWorkspaceSettings` 提供了在某些设置聚合过程中可发挥作用的详细信息。

### <a name="settings-related-apis"></a>与设置相关的 Api

- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> 读取并聚合工作区的设置。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetSettingsManager%2A> 获取 `IWorkspaceSettingsManager` 工作区的。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> 获取跨所有重叠范围聚合的给定作用域的设置。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> 包含特定范围的设置。

## <a name="workspace-suggested-practices"></a>工作区建议做法

- 返回对象 `IWorkspaceProviderFactory.CreateProvider` ，这些对象在创建时可记住其 `Workspace` 上下文。 编写提供程序接口需要在创建时保留此对象。
- 在工作区的 "本地设置" 路径内保存特定于工作区的缓存或设置。 `Microsoft.VisualStudio.Workspace.WorkspaceHelper.MakeRootedUnderWorkingFolder`在 Visual Studio 2017 版本15.6 或更高版本中使用创建文件的路径。 对于版本15.6 之前的版本，请使用以下代码片段：

```csharp
using System.IO;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static string MakeRootedUnderWorkingFolder(IWorkspace workspace, string relativePath)
{
    string workingFolder = workspace.GetSettingsManager().GetAggregatedSettings(SettingsTypes.WorkspaceControlSettings).Property<string>("WorkingFolder");
    return Path.Combine(workingFolder, relativePath);
}
```

## <a name="solution-events-and-package-auto-load"></a>解决方案事件和包自动加载

加载的包可以实现 `IVsSolutionEvents7` 和调用 `IVsSolution.AdviseSolutionEvents` 。 它包含在 Visual Studio 中打开和关闭文件夹时的事件。

UI 上下文可用于自动加载包。 该值为 `4646B819-1AE0-4E79-97F4-8A8176FDD664`。

## <a name="troubleshooting"></a>疑难解答

### <a name="the-sourceexplorerpackage-package-did-not-load-correctly"></a>SourceExplorerPackage 包未正确加载

工作区扩展性在很大程度上是基于 MEF 的，组合错误将导致承载打开文件夹的包无法加载。 例如，如果某个扩展使用导出类型 `ExportFileContextProviderAttribute` ，但该类型仅实现，则在 `IWorkspaceProviderFactory<IFileContextActionProvider>` Visual Studio 中尝试打开文件夹时会发生错误。

::: moniker range="vs-2017"

可以在 _%localappdata%\microsoft\visualstudio\15. 0_id \componentmodelcache\microsoft.visualstudio.default.err_中找到错误详细信息。 解决扩展插件实现的任何错误。

::: moniker-end

::: moniker range=">=vs-2019"

可以在 _%localappdata%\microsoft\visualstudio\16. 0_id \componentmodelcache\microsoft.visualstudio.default.err_中找到错误详细信息。 解决扩展插件实现的任何错误。

::: moniker-end

## <a name="next-steps"></a>后续步骤

* [文件上下文](workspace-file-contexts.md) -文件上下文提供程序为打开的文件夹工作区引入代码智能。
* [索引](workspace-indexing.md) 工作区索引收集并保留有关工作区的信息。
