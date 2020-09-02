---
title: 源代码管理配置详细信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7cf4a5c55e8093e5dcd6406cde1c60f642188495
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705285"
---
# <a name="source-control-configuration-details"></a>源代码管理配置详细信息
若要实现源代码管理，需要将项目系统或编辑器正确配置为执行以下操作：

- 请求转换为已更改状态的权限

- 请求保存文件的权限

- 请求在项目中添加、删除或重命名文件的权限

## <a name="request-permission-to-transition-to-changed-state"></a>请求转换为已更改状态的权限
 项目或编辑器必须通过调用来请求转换到更改 (脏) 状态的权限 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 。 在返回之前，实现的每个编辑器都 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> 必须调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 并接收从环境更改文档的批准 `True` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> 。 项目本质上是项目文件的编辑器，因此，对项目文件的实现的更改状态跟踪具有相同的责任，因为文本编辑器会对文件进行更改。 环境处理解决方案的已更改状态，但必须处理解决方案引用但不存储的任何对象（如项目文件或其项）的已更改状态。 通常，如果项目或编辑器负责管理项的持久性，则负责实现更改状态跟踪。

 为了响应 `IVsQueryEditQuerySave2::QueryEditFiles` 调用，环境可以执行以下操作：

- 拒绝对更改的调用，在这种情况下，编辑器或项目必须保持不变的 (清理) 状态。

- 指示应重新加载文档数据。 对于项目，环境将为项目重新加载数据。 编辑器必须通过其实现从磁盘重新加载数据 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> 。 在任一情况下，当重新加载数据时，项目或编辑器中的上下文都可以更改。

  这是一种复杂且困难的任务，可将适当的 `IVsQueryEditQuerySave2::QueryEditFiles` 调用改进到现有的基本代码。 因此，应在创建项目或编辑器期间集成这些调用。

## <a name="request-permission-to-save-a-file"></a>请求保存文件的权限
 在项目或编辑器保存文件之前，它必须调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> 。 对于项目文件，这些调用由解决方案自动完成，该解决方案知道何时保存项目文件。 除非的编辑器实现使用 helper 函数，否则编辑器负责进行这些调用 `IVsPersistDocData2` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 。 如果编辑器 `IVsPersistDocData2` 以这种方式实现，则将调用 `IVsQueryEditQuerySave2::QuerySaveFile` 或 `IVsQueryEditQuerySave2::QuerySaveFiles` 。

> [!NOTE]
> 始终将这些调用提前，即，当编辑器能够接收到取消时。

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>请求在项目中添加、删除或重命名文件的权限
 在项目可以添加、重命名或删除文件或目录之前，它必须调用适当的 `IVsTrackProjectDocuments2::OnQuery*` 方法来从环境请求权限。 如果授予了权限，则项目必须完成该操作，然后调用适当的 `IVsTrackProjectDocuments2::OnAfter*` 方法来通知环境操作已完成。 项目必须 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 为所有文件调用接口的方法 (例如，) 的特殊文件，而不仅仅是父文件。 文件调用是必需的，但目录调用是可选的。 如果你的项目包含目录信息，则它应调用适当的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 方法，但如果没有此信息，则环境将推断目录信息。

 项目不应 `IVsTrackProjectDocuments2` 在打开或关闭项目时调用的方法。 在启动时需要此信息的侦听器可以等待 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> 事件，并循环访问解决方案来查找所需的信息。 关机时，不需要此信息。 `IVsTrackProjectDocuments2` 是从提供的 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> 。

 对于每个添加、重命名和删除操作，都有一个 `OnQuery*` 方法和一个 `OnAfter*` 方法。 调用 `OnQuery*` 方法以请求添加、重命名或删除文件或目录的权限。 `OnAfter*`添加、重命名或删除文件或目录后，调用方法，并将项目状态反映为新状态。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
