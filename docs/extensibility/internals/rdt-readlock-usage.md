---
title: RDT_ReadLock用法 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705928"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock 用法

[_VSRDTFLAGSRDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)是一个标志，用于在正在运行的文档表 （RDT） 中锁定文档的逻辑，该表是当前在 Visual Studio IDE 中打开的所有文档的列表。 此标志确定何时打开文档，以及文档在用户界面中可见或不可见地在内存中。

通常，您使用[_VSRDTFLAGS。当](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)下列原因之一为 true 时，RDT_ReadLock：

- 您希望在不可见和只读时打开文档，但尚未确定应拥有文档。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

- 您希望提示用户保存在用户在 UI 中显示文档之前不可见地打开的文档，然后尝试将其关闭。

## <a name="how-to-manage-visible-and-invisible-documents"></a>如何管理可见文档和不可见文档

当用户在 UI 中打开文档时，必须<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>建立文档的所有者并[_VSRDTFLAGS。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>)必须设置RDT_EditLock标志。 如果无法<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>建立所有者，则当用户单击"**全部保存"** 或关闭 IDE 时，将不会保存文档。 这意味着，如果文档在内存中修改时处于不可见状态打开，并且系统会提示用户在关闭时保存文档，或者如果选择了 **"全部保存**"，则`RDT_ReadLock`无法使用。 相反，您必须使用 并在`RDT_EditLock`__VSREGDOCLOCKHOLDER时注册<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>。 [RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>)标志。

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock和文档修改

前面提到的标志表示，当用户将文档打开到可见的**DocumentWindow**`RDT_EditLock`中时，文档的不可见打开将生成其。 发生这种情况时，当可见的**文档窗口**关闭时，将显示一个**保存**提示。 `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel`最初使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager>服务的实现仅在`RDT_ReadLock`采用 时（即，当文档以不可见地打开以解析信息时）时工作。 稍后，如果必须修改文档，则锁将升级到弱**RDT_EditLock**。 如果用户随后在可见的**DocumentWindow**中打开文档，`CodeModel`则会释放的弱文档。 `RDT_EditLock`

如果用户随后关闭**DocumentWindow，** 并在提示保存打开的文档时选择 **"否**"，则`CodeModel`实现将释放文档中的所有信息，并在下次文档需要更多信息时无形中从磁盘中重新打开该文档。 此行为的微妙之处是用户打开不可见打开文档**的 DocumentWindow、** 修改文档、关闭它，然后在提示保存文档时选择 **"否**"。"的实例。 在这种情况下，如果文档有 ，`RDT_ReadLock`则文档实际上不会关闭，并且修改后的文档将在内存中不可见地保持打开状态，即使用户选择不保存文档也是如此。

如果文档的不可见打开使用弱`RDT_EditLock`，则当用户明显打开文档且没有其他锁时，它将生成其锁。 当用户关闭**DocumentWindow**并在提示保存文档时选择 **"否**"时，必须从内存中关闭文档。 这意味着不可见的客户端必须侦听 RDT 事件才能跟踪此事件。 下次需要文档时，必须重新打开该文档。
