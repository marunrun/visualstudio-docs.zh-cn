---
title: 正在保存标准文档 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198084"
---
# <a name="saving-a-standard-document"></a>保存标准文档
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

环境处理保存、 另存为，并保存所有命令。 如果用户选择**保存**，**另存为**，或**全部保存**从**文件**菜单或关闭解决方案，从而导致**保存所有**，发生以下过程。  
  
 ![标准编辑器](../../extensibility/internals/media/public.gif "公共")  
保存、 另存为和全部保存命令处理的标准编辑器  
  
 此过程详述以下步骤：  
  
1. 当**保存**并**另存为**命令当选中时，在环境中使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务以确定活动文档窗口，并应因此保存项。 活动文档窗口了解后，在环境中正在运行的 document 表的文档查找的层次结构的指针和项标识符 (itemID)。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。  
  
    当**全部保存**选择命令时，环境使用正在运行的 document 表中的信息来编译所有要保存的项的列表。  
  
2. 当解决方案收到<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>调用时，它会循环访问选定项的集 (即，公开多个选择<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务)。  
  
3. 选定内容中的每个项，该解决方案使用层次结构指针来调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>方法，以确定是否**保存**应启用菜单命令。 如果一个或多个项已更新，则**保存**启用命令。 如果在层次结构使用的标准编辑器，然后查询的层次结构委托脏状态设置为编辑器中通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>方法。  
  
4. 已更新的每个选定项，该解决方案使用层次结构指针来调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>适当的层次结构上的方法。  
  
    它是常见的层次结构以使用标准编辑器来编辑该文档。 在这种情况下，文档数据对象的编辑器应支持<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>接口。 在接收时<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>方法调用中，项目应该通知保存文档时通过调用编辑器<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A>文档数据对象上的方法。 编辑器可以允许环境来处理**另存为**对话框中的，通过调用`Query Service`为<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>接口。 这将返回一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>接口。 然后，在编辑器必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>方法，将指针传递到编辑器<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>通过实现`pPersistFile`参数。 在环境，然后执行保存操作并提供**另存为**编辑器对话框。 在环境然后回拨到编辑器<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>。  
  
5. 如果用户尝试保存一个无标题的文档 （即以前未保存的文档），则实际执行的另存为命令。  
  
6. 对于另存为命令中，环境将显示另存为对话框，提示用户输入文件的名称。  
  
    如果已更改的文件的名称，则在层次结构负责更新文档框架的缓存信息通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A>(VSFPROPID_MkDocument)。  
  
   如果**另存为**命令将该文档的位置和层次结构为敏感的文档位置，则在层次结构是负责将关闭打开的文档窗口的所有权传递给另一个层次结构。 例如，发生这种情况如果项目跟踪文件是与项目相关的内部或外部的文件 （杂项文件）。 使用以下过程来将文件的所有权更改为杂项文件项目。  
  
## <a name="changing-file-ownership"></a>更改文件所有权  
  
#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>若要将文件所有权更改为杂项文件项目  
  
1. 查询服务以获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager>接口。  
  
     一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2>返回。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A>(`pszMkDocumentNew`， `punkWindowFrame`) 方法，将文档传输到新层次结构。 层次结构执行另存为命令调用此方法。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
