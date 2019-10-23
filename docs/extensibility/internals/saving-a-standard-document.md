---
title: 保存标准文档 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: df93813d339a45689845b82fe4f5a185301b6c74
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724094"
---
# <a name="saving-a-standard-document"></a>保存标准文档
环境处理 "保存"、"另存为" 和 "保存所有" 命令。 当用户从 "**文件**" 菜单**中选择 "保存"** 、"**另存为**" 或 "全部保存" 或 "**全部保存**" 时，如果出现 "**全部保存**"，则会发生以下过程。

 ![标准编辑器](../../extensibility/internals/media/public.gif "Public")保存、保存为标准编辑器并保存所有命令处理

 以下步骤详细说明了此过程：

1. 选择 "**保存**" 和 "**另存为**" 命令时，环境将使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务来确定活动文档窗口，并因此应保存哪些项。 知道活动文档窗口后，环境将查找正在运行的文档表中文档的层次结构指针和项标识符（itemID）。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。

    如果选择了 "**全部保存**" 命令，环境将使用正在运行的文档表中的信息来编译要保存的所有项的列表。

2. 当解决方案收到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 调用时，它将循环访问选定项的集合（即，由 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务公开的多个选定项）。

3. 对于选定内容中的每一项，解决方案都使用层次结构指针来调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> 方法，以确定是否应启用 "**保存**" 菜单命令。 如果一个或多个项目已被更新，则启用**Save**命令。 如果层次结构使用标准编辑器，则层次结构会通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> 方法，将查询的脏状态委托给编辑器。

4. 在每个未更新的选定项上，解决方案使用层次结构指针对适当的层次结构调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 方法。

    层次结构通常使用标准编辑器来编辑文档。 在这种情况下，该编辑器的文档数据对象应支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 接口。 接收到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 方法调用后，项目应通过对文档数据对象调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A> 方法，通知编辑器正在保存文档。 编辑器可以通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 接口 `Query Service` 来允许环境处理 "**另存为**" 对话框。 这会返回指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 接口的指针。 然后，编辑器必须调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 方法，并通过 `pPersistFile` 参数向编辑器的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 实现传递指针。 然后，环境将执行保存操作，并提供编辑器的 "**另存为**" 对话框。 然后，环境会通过 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 回调到编辑器。

5. 如果用户尝试保存无标题文档（即以前未保存的文档），则实际执行的是 "另存为" 命令。

6. 对于 "另存为" 命令，环境会显示 "另存为" 对话框，提示用户输入文件名。

    如果该文件的名称已更改，则该层次结构负责通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A> （VSFPROPID_MkDocument）来更新文档框架的缓存信息。

   如果 "**另存为**" 命令移动文档的位置，并且层次结构对文档位置敏感，则层次结构负责将打开的文档窗口的所有权移交给其他层次结构。 例如，如果项目跟踪文件是与项目相关的内部或外部文件（杂项文件），则会发生这种情况。 使用以下过程将文件的所有权更改为杂项文件项目。

## <a name="changing-file-ownership"></a>更改文件所有权

#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>将文件所有权更改为杂项文件项目

1. @No__t_0 接口的查询服务。

     返回指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2> 的指针。

2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A> （`pszMkDocumentNew`，`punkWindowFrame`）方法将文档传输到新层次结构。 执行 "另存为" 命令的层次结构将调用此方法。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)