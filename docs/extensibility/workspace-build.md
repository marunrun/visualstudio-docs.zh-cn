---
title: Visual Studio 中的工作区生成 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 82660ee772280563b91830aaf1a18da0bc742b28
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62553323"
---
# <a name="workspace-build"></a>工作区生成

[开放式文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)方案中的生成支持需要扩展器来提供[工作区](workspaces.md)的[索引](workspace-indexing.md)和[文件上下文](workspace-file-contexts.md)数据，以及要运行的生成操作。

下面概述了你的扩展将需要的内容。

## <a name="build-file-context"></a>生成文件上下文

- 提供程序工厂
  - `ExportFileContextProviderAttribute``supportedContextTypeGuids`作为所有适用 `string` 常量的特性`BuildContextTypes`
  - 实现 `IWorkspaceProviderFactory<IFileContextProvider>`
  - 文件上下文提供程序
    - `FileContext`为每个生成操作和支持的配置返回一个
      - `contextType` 来自 <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes>
      - `context`<xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext>用 `Configuration` 属性作为生成配置来实现 (例如 `"Debug|x86"` ， `"ret"` 或（ `null` 如果不适用) ）。 或者，使用的实例 <xref:Microsoft.VisualStudio.Workspace.Build.BuildConfigurationContext> 。 配置值 **必须** 与编入索引的文件数据值的配置相匹配。

## <a name="indexed-build-file-data-value"></a>索引生成文件数据值

- 提供程序工厂
  - `ExportFileScannerAttribute``IReadOnlyCollection<FileDataValue>`作为支持的类型的属性
  - 实现 `IWorkspaceProviderFactory<IFileScanner>`
- 文件扫描器开启 `ScanContentAsync<T>`
  - 当 `FileScannerTypeConstants.FileDataValuesType` 是类型参数时返回数据
  - 返回使用构造的每个配置的文件数据值：
    - `type` 方式 `BuildConfigurationContext.ContextTypeGuid`
    - `context` 作为生成配置 (例如 `"Debug|x86"` ， `"ret"` 或（ `null` 如果不适用) ）。 此值 **必须** 与文件上下文中的配置匹配。

## <a name="build-file-context-action"></a>生成文件上下文操作

- 提供程序工厂
  - `ExportFileContextActionProvider``supportedContextTypeGuids`作为所有适用 `string` 常量的特性`BuildContextTypes`
  - 实现 `IWorkspaceProviderFactory<IFileContextActionProvider>`
- 操作提供程序 `IFileContextActionProvider.GetActionsAsync`
  - 返回一个 `IFileContextAction` 与给定的值匹配的 `FileContext.ContextType`
- 文件上下文操作
  - 实现 `IFileContextAction` 和 <xref:Microsoft.VisualStudio.Workspace.Extensions.VS.IVsCommandItem>
  - `CommandGroup` 属性返回 `16537f6e-cb14-44da-b087-d1387ce3bf57`
  - `CommandId``0x1000`用于生成、 `0x1010` 重新生成或 `0x1020` 清理

>[!NOTE]
>由于 `FileDataValue` 需要编制索引，因此在打开工作区和扫描文件以获取完整生成功能之间将有一定的时间。 第一次打开文件夹时会出现延迟，因为没有以前缓存的索引。

## <a name="reporting-messages-from-a-build"></a>从生成报告消息

生成可以通过以下两种方式之一向用户呈现信息、警告和错误消息。 简单的方法是使用 <xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService> 并提供 <xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage> ，如下所示：

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Build;

private static void OutputBuildMessage(IWorkspace workspace)
{
    IBuildMessageService buildMessageService = workspace.GetBuildMessageService();

    if (buildMessageService != null)
    {
      // Example error build message. See the documentation for BuildMessage for more information.
      var message = new BuildMessage()
      {
          Type = BuildMessage.TaskType.Error,
          Code = "MY1001",
          TaskText = "This is a sample error",
          ProjectFile = "buildfile.bld",
          File = "sourcefile.src"
          LogMessage = $"This is sample text that will only go to the Build output window pane.\n"

          // And any other properties to set
      };

      buildMessageService.ReportBuildMessages(new BuildMessage[] { message });
    }
}
```

`BuildMessage.Type` 并 `BuildMessage.LogMessage` 控制向用户显示信息的行为。 `BuildMessage.TaskType`除以外的任何值 `None` 都将生成具有给定详细信息的**错误列表**条目。 `LogMessage`将始终在**输出**工具窗口的**生成**窗格中输出。

或者，扩展可以直接与 **错误列表** 或 **生成** 窗格进行交互。 Visual Studio 2017 版本15.7 之前的版本中存在一个 bug，其中的 `pszProjectUniqueName` 参数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane2.OutputTaskItemStringEx2*> 被忽略。

>[!WARNING]
>的调用方 `IFileContextAction.ExecuteAsync` 可以为参数提供任意基础实现 `IProgress<IFileContextActionProgressUpdate>` 。 永远不会 `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` 直接调用。 目前没有使用此参数的一般准则，但这些准则可能会有所更改。

## <a name="build-related-apis"></a>生成相关 Api

- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext> 提供生成配置详细信息。
- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService><xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage>向用户显示 s。

## <a name="tasksvsjson-and-launchvsjson"></a>tasks.vs.js上的和 launch.vs.js

有关在文件上创作 tasks.vs.js或 launch.vs.js的信息，请参阅 [自定义生成和调试任务](../ide/customize-build-and-debug-tasks-in-visual-studio.md)。

## <a name="next-steps"></a>后续步骤

* [语言服务器协议](language-server-protocol.md) -了解如何将语言服务器集成到 Visual Studio 中。