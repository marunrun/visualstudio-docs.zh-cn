---
title: RDT_ReadLock Usage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c11cee4c1f8c150fc8bcf42b3dbc1a193d3441a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341354"
---
# <a name="rdtreadlock-usage"></a>RDT_ReadLock 用法

[_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)是标志，它提供逻辑来锁定文档中正在运行文档表 (RDT)，这 Visual Studio IDE 中当前打开的所有文档的列表。 此标志确定当文档处于打开状态，以及文档是否是在用户界面中可见或保持在内存中不可见的方式。

通常情况下，使用[_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)下列任一条件为 true 时：

- 你想要不可见的方式打开的文档和只读的但它尚未建立的<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>应拥有它。

- 你希望用户系统会提示保存用户在 UI 中显示，然后尝试将其关闭之前不可见的方式打开的文档。

## <a name="how-to-manage-visible-and-invisible-documents"></a>如何管理可见和不可见的文档

当用户在 UI 中，打开的文档<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>必须建立文档所有者和[_VSRDTFLAGS。RDT_EditLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>)标志必须设置。 如果没有<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>可以建立所有者，则当用户单击时，将不会保存该文档**全部保存**或关闭 IDE。 这意味着如果文档处于打开状态不可见的方式在内存中，修改和系统提示您将文档保存在关闭或保存如果用户的位置**全部保存**选择，则`RDT_ReadLock`不能使用。 相反，必须使用`RDT_EditLock`并注册<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>时[__VSREGDOCLOCKHOLDER。RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>)标志。

## <a name="rdteditlock-and-document-modification"></a>RDT_EditLock 和文档修改

提到的上一个标志指示不可见的打开的文档会产生其`RDT_EditLock`到可见由用户打开文档时**DocumentWindow**。 当发生这种情况时，用户会看到**保存**提示时可见**DocumentWindow**已关闭。 `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` 使用的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager>服务最初工作时仅`RDT_ReadLock`（即时不可见的方式打开该文档来分析信息） 执行。 更高版本，如果必须修改该文档，然后该锁将升级到为弱**RDT_EditLock**。 如果用户然后打开该文档中的可见**DocumentWindow**，则`CodeModel`的弱`RDT_EditLock`发布。

如果用户然后关闭**DocumentWindow** ，并选择**否**当系统提示你保存打开的文档，则`CodeModel`实现释放文档中的所有信息并重新打开从磁盘不可见的方式的详细信息是必需的文档的下一次的文档。 此行为的一个要点是： 用户打开的实例**DocumentWindow**的不可见的打开文档，对其进行修改，其关闭，，再选择**否**当系统提示保存文档。 在此情况下，如果该文档具有`RDT_ReadLock`，然后该文档实际上不会关闭并经过修改的文档仍处于打开状态不可见的方式在内存中，即使用户选择不保存文档。

如果不可见的打开的文档使用为弱`RDT_EditLock`，则它将产生锁定时用户打开文档以可视方式并不其他持有锁。 当用户关闭**DocumentWindow** ，并选择**否**当系统提示保存文档，然后在文档必须关闭从内存。 这意味着不可见的客户端必须侦听 RDT 事件来跟踪此匹配项。 下一次文档是必需的该文档必须重新打开。