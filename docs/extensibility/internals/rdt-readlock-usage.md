---
title: RDT_ReadLock 使用情况 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fb897fab61e1e14b52863b5853748c685200d5ba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705928"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock 用法

[_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) 是一种用于在正在运行的文档表中锁定文档的逻辑 (RDT) ，它是当前在 Visual STUDIO IDE 中打开的所有文档的列表。 此标志确定打开文档的时间，以及文档在用户界面中是否可见或在内存中保持不可见。

通常，使用 [_VSRDTFLAGS。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) 如果满足以下任一条件，则 RDT_ReadLock：

- 你希望以不可见和只读的状态打开文档，但尚未建立 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 应该拥有该文档的文档。

- 您希望在用户在 UI 中显示文档之前，提示用户保存以不可见的文档打开的文档，然后尝试将其关闭。

## <a name="how-to-manage-visible-and-invisible-documents"></a>如何管理可见和不可见的文档

当用户在用户界面中打开文档时， <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 必须建立文档的所有者并 [_VSRDTFLAGS。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>) 必须设置 RDT_EditLock 标志。 如果无法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 建立所有者，则当用户单击 " **全部保存** " 或关闭 IDE 时，将不保存该文档。 这意味着，如果文档在内存中被修改的位置以不可见的方式打开，并在选择 " **全部保存** " 时提示用户关闭或保存文档，则 `RDT_ReadLock` 无法使用。 相反，你必须使用 `RDT_EditLock` 并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 在 __VSREGDOCLOCKHOLDER 时注册 [。RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>) 标志。

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock 和文档修改

前面提到的标志表明， `RDT_EditLock` 如果文档由用户打开到可见的 **DocumentWindow**，则不可见的文档打开。 如果出现这种情况，则当隐藏**DocumentWindow**关闭时，用户将看到一个**保存**提示。 `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` 使用该服务的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> 最初仅在创建时才起作用 `RDT_ReadLock` (例如，以不可见的方式打开文档来分析信息) 。 稍后，如果必须修改文档，则锁定会升级到弱 **RDT_EditLock**。 如果用户打开了可见的 **DocumentWindow**中的文档，则 `CodeModel` 会释放的弱弱性 `RDT_EditLock` 。

如果用户关闭 **DocumentWindow** 并在系统提示保存打开的文档时选择 " **否** "，则 `CodeModel` 实现将释放文档中的所有信息，并在下次需要文档时从磁盘重新打开文档。 此行为的个很微妙是一个实例，用户在其中打开不可见的已打开文档的 **DocumentWindow** ，对其进行修改，将其关闭，然后在系统提示保存文档时选择 " **否** "。 在这种情况下，如果文档具有 `RDT_ReadLock` ，则该文档将不会实际关闭，并且修改后的文档在内存中保持打开状态，即使用户选择不保存文档也是如此。

如果文档的不可见打开使用弱弱 `RDT_EditLock` ，则当用户打开文档时，它将生成锁定，且不保留其他锁。 当用户关闭 **DocumentWindow** 并在系统提示保存文档时选择 " **否** " 时，文档必须从内存中关闭。 这意味着不可见的客户端必须侦听 RDT 事件以跟踪此事件。 下次需要该文档时，必须重新打开该文档。
