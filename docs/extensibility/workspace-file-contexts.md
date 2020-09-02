---
title: Visual Studio 中的工作区文件上下文 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 36f986db6f2c7b483b46060e1f514acc8dd9e758
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952803"
---
# <a name="workspace-file-contexts"></a>工作区文件上下文

[打开的文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)工作区中的所有见解都由实现该接口的 "文件上下文提供程序" 生成 <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> 。 这些扩展可能会查找文件夹或文件中的模式，读取 MSBuild 文件和生成文件，检测包依赖关系，等等，以便积累定义文件上下文所需的见解。 文件上下文本身不执行任何操作，而是提供另一个扩展随后可以操作的数据。

每个 <xref:Microsoft.VisualStudio.Workspace.FileContext> 都有一个 `Guid` 关联的，用于标识它所携带的数据类型。 工作区稍后使用此 `Guid` 项将其与通过属性使用数据的扩展进行匹配 <xref:Microsoft.VisualStudio.Workspace.FileContext.Context> 。 文件上下文提供程序随元数据一起导出，后者标识 `Guid` 它可能生成数据的文件上下文。

定义后，文件上下文可以与工作区中的任意数量的文件或文件夹关联。 给定的文件或文件夹可与任意数量的文件上下文相关联。 这是一个多对多关系。

文件上下文的最常见方案与生成、调试和语言服务相关。 有关详细信息，请参阅与这些方案相关的其他主题。

## <a name="file-context-lifecycle"></a>文件上下文生命周期

的生命周期 `FileContext` 是不确定的。 组件可随时异步请求某些上下文类型集。 将查询支持某些请求上下文类型子集的提供程序。 `IWorkspace`实例通过方法在使用者和提供者之间充当中间人 <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> 。 使用者可能会请求上下文，并基于上下文执行某些短期操作，而其他人可能会请求上下文并维护长期引用。

导致文件上下文过时的文件可能会发生更改。 提供程序可以在上引发事件 `FileContext` ，以通知使用者是否有更新。 例如，如果为某个文件提供了生成上下文，但磁盘上的更改使该上下文失效，则原始创建者可以调用该事件。 仍引用的任何使用者都 `FileContext` 可以重新查询新的 `FileContext` 。

>[!NOTE]
>没有对使用者的推送模式。 请求后，不会向使用者通知提供程序的新 `FileContext` 用户。

## <a name="expensive-file-context-computations"></a>成本高昂的文件上下文计算

从磁盘读取文件内容可能会消耗大量资源，尤其是在提供程序需要解析文件之间的关系时。 例如，可以查询某个提供程序的源文件的文件上下文，但文件上下文依赖于项目文件中的元数据。 分析项目文件或用 MSBuild 对其进行计算非常昂贵。 相反，扩展可以导出 `IFileScanner` 以 `FileDataValue` 在工作区索引期间创建数据。 现在，当系统询问文件上下文时， `IFileContextProvider` 可以快速查询该已索引的数据。 有关索引的详细信息，请参阅 [工作区索引](workspace-indexing.md) 主题。

>[!WARNING]
>请注意 `FileContext` ，计算的成本可能很高。 某些 UI 交互是同步的，并且依赖于大量的 `FileContext` 请求。 示例包括打开编辑器选项卡和打开 **解决方案资源管理器** 上下文菜单。 这些操作将生成许多生成上下文类型请求。

## <a name="file-context-related-apis"></a>与文件上下文相关的 Api

- <xref:Microsoft.VisualStudio.Workspace.FileContext> 保存数据和元数据。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> 和 <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider`1> 创建文件上下文。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextProviderAttribute> 导出文件上下文提供程序。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> 供使用者用于获取文件上下文。
- <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> 定义打开的文件夹将使用的生成上下文类型。

## <a name="file-context-actions"></a>文件上下文操作

`FileContext`它本身只是有关某些文件 () 的数据，而 <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> 是一种表示和处理该数据的方法。 `IFileContextAction` 在其使用中灵活。 最常见的两种情况是生成和调试。

## <a name="reporting-progress"></a>报告进度

<xref:Microsoft.VisualStudio.Workspace.IFileContextActionBase.ExecuteAsync%2A>传递方法 `IProgress<IFileContextActionProgressUpdate>` ，但不应将参数用作该类型。 `IFileContextActionProgressUpdate` 为空接口，调用 `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` 可能会引发 `NotImplementedException` 。 相反， `IFileContextAction` 必须根据方案的需要将参数强制转换为另一种类型。

有关 Visual Studio 提供的类型的信息，请参阅相应方案的文档。

## <a name="file-context-action-related-apis"></a>文件上下文操作相关 Api

- <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> 基于执行某些行为 `FileContext` 。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextActionProvider> 创建的实例 `IFileContextAction` 。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextActionProviderAttribute> 导出类型 `IWorkspaceProviderFactory<IFileContextActionProvider>` 。

## <a name="file-watching"></a>文件监视

工作区侦听文件更改通知，并通过提供 <xref:Microsoft.VisualStudio.Workspace.IFileWatcherService> <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> 。 匹配 "ExcludedItems" 设置的文件将不会生成文件通知事件。 事件间的阈值用于通知简化和减少重复。 如果需要对文件更改做出反应，应订阅此服务。

>[!TIP]
>默认情况下，工作区的 [索引服务](workspace-indexing.md) 会订阅文件事件。 文件添加和修改将导致为 `IFileScanner` 该文件的新数据调用相关的事件。 文件删除将删除索引的数据。 不需要订阅 `IFileScanner` 文件观察程序服务。

## <a name="next-steps"></a>后续步骤

* [索引](workspace-indexing.md) 工作区索引收集并保留有关工作区的信息。
* [工作](workspaces.md) 区-查看工作区概念和设置存储。
