---
title: 在 Visual Studio 中的工作区生成 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 82660ee772280563b91830aaf1a18da0bc742b28
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62553323"
---
# <a name="workspace-build"></a>工作区生成

支持构建[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)方案需求要求您的扩展程序提供[编制索引](workspace-indexing.md)并[文件上下文](workspace-file-contexts.md)数据[工作区](workspaces.md)，作为以及要运行的生成操作。

下面是您的扩展插件将需要的概述。

## <a name="build-file-context"></a>生成文件上下文

- 提供程序工厂
  - `ExportFileContextProviderAttribute` 属性与`supportedContextTypeGuids`为所有适用`string`从常量 `BuildContextTypes`
  - 实现 `IWorkspaceProviderFactory<IFileContextProvider>`
  - 文件上下文提供程序
    - 返回`FileContext`为每个生成操作和支持的配置
      - `contextType` 从 <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes>
      - `context` 实现<xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext>与`Configuration`属性设置为生成配置 (例如`"Debug|x86"`， `"ret"`，或`null`如果不适用)。 或者，使用的实例<xref:Microsoft.VisualStudio.Workspace.Build.BuildConfigurationContext>。 配置值**必须**匹配索引的文件数据值中的配置。

## <a name="indexed-build-file-data-value"></a>索引的生成文件的数据值

- 提供程序工厂
  - `ExportFileScannerAttribute` 属性与`IReadOnlyCollection<FileDataValue>`为支持的类型
  - 实现 `IWorkspaceProviderFactory<IFileScanner>`
- 在文件扫描程序 `ScanContentAsync<T>`
  - 返回数据时`FileScannerTypeConstants.FileDataValuesType`是类型参数
  - 返回用来构造每个配置的文件数据值：
    - `type` 为 `BuildConfigurationContext.ContextTypeGuid`
    - `context` 作为生成配置 (例如`"Debug|x86"`， `"ret"`，或`null`如果不适用)。 此值**必须**匹配的文件上下文中的配置。

## <a name="build-file-context-action"></a>生成文件上下文操作

- 提供程序工厂
  - `ExportFileContextActionProvider` 属性与`supportedContextTypeGuids`为所有适用`string`从常量 `BuildContextTypes`
  - 实现 `IWorkspaceProviderFactory<IFileContextActionProvider>`
- 上的操作提供程序 `IFileContextActionProvider.GetActionsAsync`
  - 返回`IFileContextAction`相匹配给定`FileContext.ContextType`值
- 文件上下文操作
  - 实现`IFileContextAction`和 <xref:Microsoft.VisualStudio.Workspace.Extensions.VS.IVsCommandItem>
  - `CommandGroup` 属性返回 `16537f6e-cb14-44da-b087-d1387ce3bf57`
  - `CommandId` 是`0x1000`对于生成，`0x1010`重新生成，或`0x1020`对于清除

>[!NOTE]
>由于`FileDataValue`需要编制索引，将有一定量的打开的工作区和完全生成功能扫描该文件的点之间的时间。 延迟将出现在第一个打开的文件夹，因为没有以前缓存的索引。

## <a name="reporting-messages-from-a-build"></a>从生成的报告消息

生成可传达的信息、 警告和错误消息给用户两种方式之一。 简单的方法是使用<xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService>，并提供<xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage>，如下所示：

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

`BuildMessage.Type` 和`BuildMessage.LogMessage`控制行为的信息提供给用户的位置。 任何`BuildMessage.TaskType`值，而`None`将生成**错误列表**条目与给定的详细信息。 `LogMessage` 始终会在输出**构建**窗格**输出**工具窗口。

或者，扩展可以直接与交互**错误列表**或**生成**窗格。 Visual Studio 2017 版本 15.7 之前的版本中存在一个 bug 其中`pszProjectUniqueName`自变量的<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane2.OutputTaskItemStringEx2*>将被忽略。

>[!WARNING]
>调用方`IFileContextAction.ExecuteAsync`可以提供任意基础实现`IProgress<IFileContextActionProgressUpdate>`参数。 永远不会调用`IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)`直接。 目前有通用准则使用此参数，但这些准则可能会有所变动。

## <a name="build-related-apis"></a>生成相关的 Api

- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext> 提供了生成配置详细信息。
- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService> 显示<xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage>的用户。

## <a name="tasksvsjson-and-launchvsjson"></a>tasks.vs.json 和 launch.vs.json

有关创作的 tasks.vs.json 或 launch.vs.json 文件的信息，请参阅[自定义生成和调试任务](../ide/customize-build-and-debug-tasks-in-visual-studio.md)。

## <a name="next-steps"></a>后续步骤

* [语言服务器协议](language-server-protocol.md)-了解如何集成到 Visual Studio 语言服务器。