---
title: 保存标准文档 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e8d50a9e62e69f925564717020a51f88620f5f3b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705555"
---
# <a name="saving-a-standard-document"></a>保存标准文档
环境处理"保存、保存为"和"保存所有"命令。 当用户选择 **"保存**"、"**保存为**"或从 **"文件"** 菜单中**保存全部**内容或关闭解决方案，从而导致 **"全部保存**"时，将发生以下过程。

 ![标准编辑器](../../extensibility/internals/media/public.gif "Public")为标准编辑器保存、保存为和保存所有命令处理

 此过程在以下步骤中进行了详细说明：

1. 选择 **"保存****和保存为"** 命令时，环境将使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>该服务来确定活动文档窗口，从而确定应保存哪些项。 知道活动文档窗口后，环境在正在运行的文档表中查找文档的层次结构指针和项标识符 （itemID）。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。

    选择"**全部保存"** 命令后，环境将使用正在运行的文档表中的信息编译要保存的所有项的列表。

2. 当解决方案收到呼叫时<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>，它会通过所选项集（即<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务公开的多个选择）进行遍接。

3. 在所选内容中的每个项上，解决方案使用层次结构指针调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>方法来确定是否应启用 **"保存**菜单"命令。 如果一个或多个项目脏，则启用 **"保存**"命令。 如果层次结构使用标准编辑器，则层次结构通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>方法将查询脏状态的层次结构委托给编辑器。

4. 在每个脏的选定项上，解决方案使用层次结构指针在适当的层次结构上调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>方法。

    层次结构通常使用标准编辑器编辑文档。 在这种情况下，该编辑器的文档数据对象应支持该<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>接口。 收到<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>方法调用后，项目应通过在文档数据对象上调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A>方法来通知编辑器文档正在保存。 编辑器可以通过调用`Query Service`<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>接口来允许环境处理 **"另存即"** 对话框。 这将返回指向接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>指针。 然后，编辑器必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>方法，通过<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>`pPersistFile`参数传递指向编辑器实现的指针。 然后，环境执行"保存"操作，并为编辑器提供 **"另存为**"对话框。 然后，环境使用<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>调用回编辑器。

5. 如果用户尝试保存无标题文档（即以前未保存的文档），则实际执行"保存为"命令。

6. 对于"保存为"命令，环境将显示"另存为"对话框，提示用户输入文件名。

    如果文件的名称已更改，则层次结构负责通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A>（VSFPROPID_MkDocument）更新文档帧的缓存信息。

   如果 **"保存为"** 命令移动文档的位置，并且层次结构对文档位置很敏感，则层次结构负责将打开的文档窗口的所有权移交给其他层次结构。 例如，如果项目跟踪文件是与项目相关的内部文件还是外部文件（杂项文件），则会发生这种情况。 使用以下过程将文件的所有权更改为"杂项文件"项目。

## <a name="changing-file-ownership"></a>更改文件所有权

#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>将文件所有权更改为"杂项文件"项目

1. 查询接口的服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager>。

     返回指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2>的指针。

2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A>（`pszMkDocumentNew` `punkWindowFrame`） 方法以将文档传输到新层次结构。 执行"保存为"命令的层次结构调用此方法。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
