---
title: 文档锁持有者管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 73c6151b5c02cb81a10c2725091c16457db70e33
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204633"
---
# <a name="document-lock-holder-management"></a>文档锁持有者管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

运行文档表 (RDT) 维护打开的文档和它们具有的任何编辑锁的计数。 以编程方式编辑在后台，而用户看到在文档窗口中打开的文档时，您可以编辑锁放置 RDT 中的文档。 通过修改通过图形用户界面的多个文件的设计人员通常使用此功能。  
  
## <a name="document-lock-holder-scenarios"></a>文档锁持有者方案  
  
### <a name="file-a-has-a-dependence-on-file-b"></a>文件"a"具有的依赖文件"b"  
 假设你在其中实施的标准编辑器"A"的文件类型"a"、 和类型"a"具有对引用 （或依赖关系） 的每个文件类型"b"的文件。 标准编辑器"B"存在"b"类型的文件。 当编辑器"A"打开文件时"a"检索到相应的文件"b"的引用。 不显示文件"b"，但编辑器"A"可以对其进行修改。 编辑器"A"到文件的文档数据的引用"b"从获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>方法和还维护文件"b"上的编辑锁。 编辑器"A"完成操作后修改文件"b"可以递减编辑锁计数文件"b"通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A>方法。 如果已调用，则可以忽略此步骤<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>方法使用参数`dwRDTLockType`设置为<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>。  
  
### <a name="file-b-is-opened-by-a-different-editor"></a>另一个编辑器打开文件"b"  
 在的"b"文件已打开编辑器"B"编辑器"A"尝试将其打开时，有两个不同的方案来处理：  
  
- 如果在兼容的编辑器中打开文件"b"，您必须具有编辑器"A"注册"b"文件使用的文档编辑锁<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A>方法。 文档中取消注册你的编辑器"A"完成修改文件"b"后，编辑锁定使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A>方法。  
  
- 如果不兼容的方式打开文件"b"，您可以让尝试的打开文件"b"编辑器"A"失败，或者您可以让使用编辑器"A"部分打开并显示相应的错误消息相关联的视图。 错误消息应指示用户在不兼容的编辑器中关闭文件"b"，然后重新打开"a"使用文件编辑器"A"。 您还可以实现[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A>提示用户关闭文件"b"不兼容的编辑器中打开的。 如果用户关闭文件"b"，打开文件"a"中编辑器"A"将继续正常进行。  
  
## <a name="additional-document-edit-lock-considerations"></a>其他文档编辑锁定注意事项  
 如果编辑器"A"是唯一具有编辑文件"b"上的锁不是像"B"编辑器还包含一个文档的文档的编辑器编辑文件"b"上的锁，获得不同的行为。 在中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，**类设计器**是不保持关联的代码文件的编辑锁的可视化设计器的示例。 也就是说，如果用户已在设计视图中打开类图，并且同时，打开关联的代码文件时，如果用户修改代码文件，但不会保存所做的更改，所做的更改也会丢失到类图 (.cd) 文件。 如果**类设计器**具有唯一的文档编辑代码文件锁定，不会要求用户以保存所做的更改，关闭代码文件时。 IDE 将要求用户保存所做的更改只有在用户关闭后才**类设计器**。 已保存的更改将反映在这两个文件。 如果这两个**类设计器**和代码文件编辑器代码文件中，在保存文档编辑锁定，然后系统会提示用户保存关闭代码文件或窗体时。 此时已保存的更改将反映在窗体和代码文件。 类图的详细信息，请参阅[使用类图 （类设计器）](../ide/working-with-class-diagrams-class-designer.md)。  
  
 请注意，是否你需要编辑锁置于非编辑器的文档，则必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>接口。  
  
 很多时候一个 UI 设计器，以编程方式修改代码文件会对多个文件进行更改。 在这种情况下<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A>方法可处理通过一个或多个文档的保存**你想要将更改保存到以下各项？** 对话框。  
  
## <a name="see-also"></a>请参阅  
 [运行文档表](../extensibility/internals/running-document-table.md)   
 [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
