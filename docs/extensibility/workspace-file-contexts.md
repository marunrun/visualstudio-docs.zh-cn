---
title: 在 Visual Studio 中的工作区文件上下文 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 36f986db6f2c7b483b46060e1f514acc8dd9e758
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952803"
---
# <a name="workspace-file-contexts"></a>工作区文件上下文

所有见解[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)工作区生成的"文件上下文提供程序"的实现<xref:Microsoft.VisualStudio.Workspace.IFileContextProvider>接口。 这些扩展可能会查找文件夹中的模式或文件，读取的 MSBuild 文件以及生成文件，检测到的包依赖项等要累积定义文件上下文所需的见解。 文件上下文本身不执行任何操作，而是提供另一个扩展可以操作的数据。

每个<xref:Microsoft.VisualStudio.Workspace.FileContext>具有`Guid`与之关联的标识的数据类型它携带。 工作区使用此`Guid`更高版本才能与使用的数据通过扩展匹配其<xref:Microsoft.VisualStudio.Workspace.FileContext.Context>属性。 与标识的文件上下文的元数据一起导出的文件上下文提供程序`Guid`s 其可能产生的数据。

定义后，可以与任意数量的文件或文件夹的工作区中相关联的文件上下文。 给定的文件或文件夹可以包含任意数量的文件上下文相关联。 它是多对多关系。

与生成、 调试和语言服务相关的文件上下文最常见的方案。 有关详细信息，请参阅相关的这些方案的其他主题。

## <a name="file-context-lifecycle"></a>文件上下文生命周期

为生命周期`FileContext`非确定性函数。 在任何时候，组件可以以异步方式请求上下文类型的一些组。 将查询支持的请求上下文类型的一些子集的提供程序。 `IWorkspace`实例充当中间人之间的使用者和提供程序通过<xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A>方法。 使用者可能会请求上下文和执行某些基于上下文，而其他人可能会请求上下文并维护且生存期较长的引用的短期操作。

可能会导致文件上下文过时的文件发生更改。 提供程序可以引发一个事件上`FileContext`以通知使用者的更新。 例如，如果生成上下文提供的一些文件，但磁盘上的更改使该上下文，原始制造者可以调用该事件。 仍会引用的任何使用者`FileContext`可以然后重新用于新查询`FileContext`。

>[!NOTE]
>没有向使用者推送模型。 使用者将不会收到提供程序的新`FileContext`之后他们的请求。

## <a name="expensive-file-context-computations"></a>成本高昂的文件上下文计算

从磁盘读取文件内容可能很昂贵，尤其是当提供程序需要解决文件之间的关系。 例如，一个提供程序可能会查询的一些源文件的文件上下文，但文件上下文是依赖于来自项目文件的元数据。 正在分析项目文件或对其进行评估使用 MSBuild 成本很高。 相反，扩展可以将导出`IFileScanner`若要创建`FileDataValue`工作区索引期间的数据。 现在系统要求进行文件上下文时`IFileContextProvider`可以快速查询该索引的数据。 有关索引的详细信息，请参阅[工作区索引](workspace-indexing.md)主题。

>[!WARNING]
>谨慎的其他方法的你`FileContext`可能成本计算。 某些 UI 交互都是同步的并且依赖于大量的`FileContext`请求。 示例包括打开编辑器选项卡并打开**解决方案资源管理器**上下文菜单。 这些操作，请键入请求的多个生成上下文。

## <a name="file-context-related-apis"></a>文件上下文相关的 Api

- <xref:Microsoft.VisualStudio.Workspace.FileContext> 保存数据和元数据。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> 和<xref:Microsoft.VisualStudio.Workspace.IFileContextProvider`1>创建文件上下文。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextProviderAttribute> 将导出文件上下文提供程序。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> 用于使用者以获取文件的上下文。
- <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> 定义将使用打开的文件夹的生成上下文类型。

## <a name="file-context-actions"></a>文件上下文操作

虽然`FileContext`本身是有关一些文件，只是数据<xref:Microsoft.VisualStudio.Workspace.IFileContextAction>是 express 和操作该数据的方法。 `IFileContextAction` 是灵活的使用量。 两个最常见的情况是构建和调试。

## <a name="reporting-progress"></a>报告进度

<xref:Microsoft.VisualStudio.Workspace.IFileContextActionBase.ExecuteAsync%2A>方法传递`IProgress<IFileContextActionProgressUpdate>`，但不应与该类型使用参数。 `IFileContextActionProgressUpdate` 是一个空接口，并调用`IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)`可能会引发`NotImplementedException`。 相反，`IFileContextAction`必须转换根据方案的另一种类型的参数。

由 Visual Studio 提供的类型的信息，请参阅各自方案的文档。

## <a name="file-context-action-related-apis"></a>与 Api 相关的文件上下文操作

- <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> 执行基于某些行为`FileContext`。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextActionProvider> 创建的实例`IFileContextAction`。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextActionProviderAttribute> 将类型导出`IWorkspaceProviderFactory<IFileContextActionProvider>`。

## <a name="file-watching"></a>文件监视

工作区文件更改通知进行侦听，并提供<xref:Microsoft.VisualStudio.Workspace.IFileWatcherService>通过<xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A>。 匹配的"ExcludedItems"设置文件将不会生成文件通知事件。 事件之间的阈值用于通知简化和减少重复。 当需要对文件更改做出反应时，应订阅此服务。

>[!TIP]
>工作区[索引服务](workspace-indexing.md)默认情况下文件事件订阅。 文件添加和修改将导致相关`IFileScanner`的事件要调用的该文件的新数据。 文件删除操作将删除索引的数据。 无需订阅你`IFileScanner`到文件观察程序服务。

## <a name="next-steps"></a>后续步骤

* [索引](workspace-indexing.md)-工作区索引收集和保留的工作区的信息。
* [工作区](workspaces.md)-查看工作区的概念和设置存储。
