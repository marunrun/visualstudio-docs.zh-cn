---
title: 保存标准文档 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5040070287db6486fa62c9010fe023be31b04cbe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198084"
---
# <a name="saving-a-standard-document"></a>保存标准文档
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

环境处理 "保存"、"另存为" 和 "保存所有" 命令。 当用户从 "**文件**" 菜单**中选择 "保存"**、"**另存为**" 或 "全部保存" 或 "**全部保存**" 时，如果出现 "**全部保存**"，则会发生以下过程。  
  
 ![标准编辑器](../../extensibility/internals/media/public.gif "公用")  
保存、保存为标准编辑器并保存所有命令处理  
  
 以下步骤详细说明了此过程：  
  
1. 选择 " **保存** " 和 " **另存为** " 命令时，环境将使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务来确定活动文档窗口，并因此应保存哪些项。 已知活动文档窗口后，环境将查找正在运行的文档表中文档 (itemID) 的层次结构指针和项标识符。 有关详细信息，请参阅 [运行文档表](../../extensibility/internals/running-document-table.md)。  
  
    如果选择了 " **全部保存** " 命令，环境将使用正在运行的文档表中的信息来编译要保存的所有项的列表。  
  
2. 当解决方案接收到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 调用时，它将循环访问所选项集， (即服务公开的多个选择 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>) 。  
  
3. 对于选定内容中的每一项，解决方案都使用层次结构指针来调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> 方法，以确定是否应启用 " **保存** " 菜单命令。 如果一个或多个项目已被更新，则启用 **Save** 命令。 如果层次结构使用标准编辑器，则层次结构会通过调用方法，将查询的脏状态委托给编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> 。  
  
4. 在每个未更新的选定项上，解决方案使用层次结构指针对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 适当的层次结构调用方法。  
  
    层次结构通常使用标准编辑器来编辑文档。 在这种情况下，该编辑器的文档数据对象应支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 接口。 接收到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 方法调用后，该项目应通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A> 对文档数据对象调用方法，通知编辑器正在保存文档。 编辑器可以通过调用接口，允许环境处理 " **另存为** " 对话框 `Query Service` <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 。 这会返回一个指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 。 然后，编辑器必须调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 方法，并通过参数将指针传递到编辑器的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 实现 `pPersistFile` 。 然后，环境将执行保存操作，并提供编辑器的 " **另存为** " 对话框。 然后，环境通过回调到编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 。  
  
5. 如果用户尝试保存无标题文档 (即，先前未保存的文档) ，则实际执行的是 "另存为" 命令。  
  
6. 对于 "另存为" 命令，环境会显示 "另存为" 对话框，提示用户输入文件名。  
  
    如果该文件的名称已更改，则层次结构负责通过调用 (VSFPROPID_MkDocument) 来更新文档框架的缓存信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A> 。  
  
   如果 " **另存为** " 命令移动文档的位置，并且层次结构对文档位置敏感，则层次结构负责将打开的文档窗口的所有权移交给其他层次结构。 例如，如果项目跟踪文件是否是内部或外部文件 (与项目相关的杂项文件) ，则会发生这种情况。 使用以下过程将文件的所有权更改为杂项文件项目。  
  
## <a name="changing-file-ownership"></a>更改文件所有权  
  
#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>将文件所有权更改为杂项文件项目  
  
1. 接口的查询服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> 。  
  
     返回指向的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A> (`pszMkDocumentNew` ， `punkWindowFrame`) 方法将文档传输到新层次结构。 执行 "另存为" 命令的层次结构将调用此方法。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
