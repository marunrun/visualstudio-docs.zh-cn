---
title: 文档锁持有者管理 |Microsoft Docs
description: 了解如何对正在运行的文档表中的文档设置编辑锁定，而用户在文档窗口中看不到打开的文档。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: c15696d81be92f0549069bad354e65356f7b2e7c
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995897"
---
# <a name="document-lock-holder-management"></a>文档锁持有者管理

正在运行的文档表 (RDT) 维护打开的文档和它们所拥有的所有编辑锁的计数。 可以在后台以编程方式编辑 RDT 中的文档时，对其进行编辑锁定，而无需用户在文档窗口中查看打开的文档。 此功能通常由通过图形用户界面修改多个文件的设计器使用。

## <a name="document-lock-holder-scenarios"></a>文档锁持有者方案

### <a name="file-a-has-a-dependence-on-file-b"></a>文件 "a" 依赖于文件 "b"

请考虑这样一种情况：您为文件类型 "a" 实现了标准编辑器 "A"，并且 "a" 类型的每个文件都有一个对 "b" 类型的文件的 (或) 依赖项的引用。 对于类型为 "b" 的文件，存在标准编辑器 "B"。 当编辑器 "A" 打开文件 "a" 时，它会检索对相应文件 "b" 的引用。 文件 "b" 未显示，但编辑器 "A" 可以修改它。 编辑器 "A" 从方法获取对文件 "b" 的文档数据的引用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> ，还会在文件 "b" 上保留编辑锁定。 在编辑器 "A" 完成对文件 "b" 的修改后，可以通过调用方法来减小文件 "b" 上的编辑锁计数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> 。 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> 参数 `dwRDTLockType` 设置为 _VSRDTFLAGS 的情况下调用了方法，则可以省略此步骤 [。RDT_NoLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_NoLock>)。

### <a name="file-b-is-opened-by-a-different-editor"></a>文件 "b" 由不同的编辑器打开

如果编辑器 "A" 尝试打开文件 "b" 时，文件 "b" 已打开，则可以通过两种不同的方案来处理：

- 如果文件 "b" 在兼容的编辑器中打开，则必须在 "A" 上使用方法在文件 "b" 上注册文档编辑锁定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> 。 在编辑器 "A" 完成对文件 "b" 的修改后，使用方法取消注册文档编辑锁定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A> 。

- 如果文件 "b" 是以不兼容的方式打开的，则可以让编辑器 "A" 尝试打开文件 "b"，也可以让与编辑器 "A" 相关联的视图部分打开并显示相应的错误消息。 错误消息应指示用户关闭不兼容的编辑器中的文件 "b"，然后使用编辑器 "A" 重新打开文件 "a"。 您还可以实现 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A> 以提示用户关闭不兼容编辑器中打开的文件 "b"。 如果用户关闭文件 "b"，则在编辑器中打开文件 "a" 会正常继续。

## <a name="additional-document-edit-lock-considerations"></a>其他文档编辑锁定注意事项

如果编辑器 "A" 是在文件 "b" 上具有文档编辑锁定的唯一编辑器，而不是在编辑器 "B" 中也持有文件 "b" 上的文档编辑锁定，则会获得不同的行为。 在中 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ， **类设计器** 是一个可视化设计器的示例，该设计器在关联的代码文件上不持有编辑锁。 也就是说，如果用户在 "设计" 视图中打开一个类图并同时打开关联的代码文件，并且用户修改了代码文件但未保存所做的更改，则这些更改也会丢失到类关系图 ( cd) 文件中。 如果 **类设计器** 在代码文件上只有文档编辑锁定，则在关闭代码文件时不会要求用户保存更改。 IDE 会要求用户在用户关闭 **类设计器** 后保存更改。 保存的更改将反映在这两个文件中。 如果 **类设计器** 和代码文件编辑器持有代码文件的文档编辑锁定，则关闭代码文件或窗体时，系统将提示用户保存。 此时，保存的更改将同时反映在窗体和代码文件中。 有关类图的详细信息，请参阅 [使用类图 (类设计器) ](../ide/class-designer/designing-and-viewing-classes-and-types.md)。

请注意，如果需要对非编辑器的文档放置编辑锁定，则必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 接口。

很多时候，以编程方式修改代码文件的 UI 设计器也会对多个文件进行更改。 在这种情况下， <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A> 方法通过 " **是否要保存对以下项的更改？** " 对话框处理一个或多个文档的保存。

## <a name="see-also"></a>另请参阅

- [运行文档表](../extensibility/internals/running-document-table.md)
- [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
