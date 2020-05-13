---
title: 源代码管理配置详细信息 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705285"
---
# <a name="source-control-configuration-details"></a>源代码管理配置详细信息
为了实现源代码管理，您需要正确配置项目系统或编辑器，以便执行以下操作：

- 请求将转换到已更改状态的权限

- 请求保存文件的权限

- 请求在项目中添加、删除或重命名文件的权限

## <a name="request-permission-to-transition-to-changed-state"></a>请求将转换到更改状态的权限
 项目或编辑器必须通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>请求请求转换为已更改的（脏）状态。 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A>的每个编辑器都必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>并收到批准才能从环境中更改文档，然后才能返回`True`。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> 项目本质上是项目文件的编辑器，因此，与文本编辑器对其文件执行更改状态跟踪具有相同的责任。 环境处理解决方案的更改状态，但必须处理解决方案引用但不存储的任何对象的更改状态，如项目文件或其项。 通常，如果项目或编辑器负责管理项目的持久性，则负责实现更改状态跟踪。

 为了响应调用，`IVsQueryEditQuerySave2::QueryEditFiles`环境可以执行以下操作：

- 拒绝更改调用，在这种情况下，编辑器或项目必须保持未更改（干净）状态。

- 指示应重新加载文档数据。 对于项目，环境将重新加载项目的数据。 编辑器必须通过磁盘<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>实现重新加载数据。 在这两种情况下，项目或编辑器中的上下文都可以在重新加载数据时更改。

  将适当的`IVsQueryEditQuerySave2::QueryEditFiles`调用改装到现有代码库是一项复杂而艰巨的任务。 因此，应在创建项目或编辑器期间集成这些调用。

## <a name="request-permission-to-save-a-file"></a>请求保存文件的权限
 在项目或编辑器保存文件之前，它必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>。 对于项目文件，这些调用由解决方案自动完成，解决方案知道何时保存项目文件。 编辑器负责进行这些调用，除非编辑器实现`IVsPersistDocData2`使用帮助器函数。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 如果编辑器以这种方式实现`IVsPersistDocData2`，则调用`IVsQueryEditQuerySave2::QuerySaveFile`或`IVsQueryEditQuerySave2::QuerySaveFiles`为您进行调用。

> [!NOTE]
> 始终先发制人地拨打这些呼叫，即，在编辑能够收到取消时。

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>请求在项目中添加、删除或重命名文件的权限
 在项目可以添加、重命名或删除文件或目录之前，它必须调用适当的`IVsTrackProjectDocuments2::OnQuery*`方法来请求环境的权限。 如果授予权限，则项目必须完成该操作，然后调用适当的`IVsTrackProjectDocuments2::OnAfter*`方法来通知环境操作已完成。 项目必须调用所有文件的<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>接口方法（例如，特殊文件），而不仅仅是父文件。 文件调用是必填项，但目录调用是可选的。 如果项目具有目录信息，则应调用适当的<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>方法，但如果它没有此信息，则环境将推断目录信息。

 项目不应调用 项目打开或关闭`IVsTrackProjectDocuments2`时的方法。 在启动时想要此信息的侦听器可以等待<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>事件并遍遍解决方案以查找所需的信息。 关闭时，不需要此信息。 `IVsTrackProjectDocuments2`从 提供<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>。

 对于每个添加、重命名和删除操作，都有一个`OnQuery*`方法和一个`OnAfter*`方法。 调用`OnQuery*`方法以请求添加、重命名或删除文件或目录的权限。 在`OnAfter*`添加、重命名或删除文件或目录并删除项目状态后调用 方法，并反映新状态。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
