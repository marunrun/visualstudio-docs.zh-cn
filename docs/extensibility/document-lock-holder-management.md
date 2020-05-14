---
title: 文档锁持有人管理 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9dd520f8ad5cab1f0cfee890c4bcc388c204bb1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712125"
---
# <a name="document-lock-holder-management"></a>文档锁持有人管理

正在运行的文档表 （RDT） 维护打开的文档及其拥有的任何编辑锁的计数。 当用户在后台以编程方式编辑文档时，可以在 RDT 中放置编辑锁，而用户却看不到文档窗口中打开的文档。 通过图形用户界面修改多个文件的设计人员通常使用此功能。

## <a name="document-lock-holder-scenarios"></a>文档锁定持有人方案

### <a name="file-a-has-a-dependence-on-file-b"></a>文件"a"依赖于文件"b"

请考虑以下情况：对于文件类型"a"实现标准编辑器"A"，并且类型为"a"的每个文件都引用（或依赖）类型为"b"的文件。 对于类型为"b"的文件，存在标准编辑器"B"。 当编辑器"A"打开文件"a"时，它会检索对相应文件"b"的引用。 文件"b"不显示，但编辑器"A"可以修改它。 编辑器"A"从该方法获取对文件"b"的文档数据的引用，<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>并维护文件"b"的编辑锁。 编辑"A"修改完文件"b"后，可以通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A>方法来减少文件"b"的编辑锁计数。 如果将参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>`dwRDTLockType`设置为_VSRDTFLAGS调用方法，则可以省略此步骤[。RDT_NoLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_NoLock>).

### <a name="file-b-is-opened-by-a-different-editor"></a>文件"b"由不同的编辑器打开

如果编辑"B"尝试打开文件"B"时，编辑"B"已经打开该文件"b"，则有两个单独的方案需要处理：

- 如果文件"b"在兼容编辑器中打开，则必须让编辑器"A"使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A>注册文件"b"的文档编辑锁。 编辑"A"修改文件"b"后，使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A>取消注册文档编辑锁。

- 如果文件"b"以不兼容的方式打开，则可以让编辑"A"尝试打开文件"b"失败，也可以让与编辑器"A"关联的视图部分打开并显示相应的错误消息。 错误消息应指示用户关闭不兼容编辑器中的文件"b"，然后使用编辑器"A"重新打开文件"a"。 还可以实现该方法[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A>以提示用户关闭在不兼容编辑器中打开的文件"b"。 如果用户关闭文件"b"，则编辑器"A"中文件"a"的打开将正常进行。

## <a name="additional-document-edit-lock-considerations"></a>其他文档编辑锁定注意事项

如果编辑器"A"是文件"b"上唯一具有文档编辑锁的编辑器，则您会获得不同的行为，如果编辑器"B"对文件"b"也持有文档编辑锁，则不同。 在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]中，**类设计器**是可视化设计器的示例，该设计器不持有关联的代码文件上的编辑锁。 也就是说，如果用户在设计视图中打开了类图，并且关联的代码文件同时打开，如果用户修改了代码文件但不保存更改，则更改也会丢失到类关系图 （.cd） 文件。 如果**类设计器**在代码文件上具有唯一的文档编辑锁，则在关闭代码文件时不会要求用户保存更改。 IDE 要求用户仅在用户关闭**类设计器**后保存更改。 保存的更改将反映在两个文件中。 如果**类设计器**和代码文件编辑器都持有代码文件上的文档编辑锁，则在关闭代码文件或窗体时，系统会提示用户保存。 此时，保存的更改将反映在窗体和代码文件中。 有关类关系图的详细信息，请参阅[使用类关系图（类设计器）。](../ide/class-designer/designing-and-viewing-classes-and-types.md)

请注意，如果需要在非编辑器的文档上放置编辑锁，则必须实现该<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>接口。

很多时候，以编程方式修改代码文件的 UI 设计器对多个文件进行更改。 在这种情况下，<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A>该方法通过"**是否要保存对以下项的更改？"** 对话框来处理一个或多个文档的保存。

## <a name="see-also"></a>请参阅

- [正在运行文档表](../extensibility/internals/running-document-table.md)
- [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
