---
title: RDT_ReadLock 使用情况 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9a6b5f86f0cfbb71f6264bdc74df72ad9209c9d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154129"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock 用法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 一个标志，该标志提供用于锁定正在运行的文档表中的文档的逻辑 (RDT) ，该列表是当前在 Visual Studio IDE 中打开的所有文档的列表。 此标志确定打开文档的时间，以及文档在用户界面中是否可见或在内存中保持不可见。  
  
 通常， <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 如果满足以下条件之一，则使用：  
  
- 如果要以不可见和只读的状态打开文档，但尚未建立 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 应该拥有该文档的文档。  
  
- 当你希望系统提示用户保存在用户将其显示在 UI 中之前打开的文档，然后尝试将其关闭。  
  
## <a name="how-to-manage-visible-and-invisible-documents"></a>如何管理可见和不可见的文档  
 当用户在用户界面中打开文档时， <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 必须建立文档的所有者，并且 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 必须设置一个标志。 如果无法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 建立所有者，则当用户单击 " **全部保存** " 或关闭 IDE 时，将不保存该文档。 这意味着，如果文档在内存中被修改的位置以不可见的方式打开，并在选择 " **全部保存** " 时提示用户关闭或保存文档，则 `RDT_ReadLock` 无法使用。 相反，你必须使用 `RDT_EditLock` 并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 在标志时注册 <xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER> 。  
  
## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock 和文档修改  
 前面提到的标志表明， `RDT_EditLock` 如果文档由用户打开到可见的 **DocumentWindow**，则不可见的文档打开。 如果出现这种情况，则当隐藏**DocumentWindow**关闭时，用户将看到一个**保存**提示。 使用该服务的 VisualStudio 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> 最初仅在 (时才起作用 `RDT_ReadLock` ，即，以不可见的方式打开文档来) 分析信息。 稍后，如果必须修改文档，则锁定会升级到弱 **RDT_EditLock**。 如果用户打开了可见的 **DocumentWindow**中的文档，则 `CodeModel` 会释放的弱弱性 `RDT_EditLock` 。  
  
 如果用户关闭 **DocumentWindow** 并在系统提示保存打开的文档时选择 " **否** "，则 `CodeModel` 实现将释放文档中的所有信息，并在下次需要文档时从磁盘重新打开文档。 此行为的个很微妙是一个实例，用户在其中打开不可见的已打开文档的 **DocumentWindow** ，对其进行修改，将其关闭，然后在系统提示保存文档时选择 " **否** "。 在这种情况下，如果文档具有 `RDT_ReadLock` ，则该文档将不会实际关闭，并且修改后的文档在内存中保持打开状态，即使用户选择不保存文档也是如此。  
  
 如果文档的不可见打开使用弱弱 `RDT_EditLock` ，则当用户打开文档时，它将生成锁定，且不保留其他锁。 当用户关闭 **DocumentWindow** 并在系统提示保存文档时选择 " **否** " 时，文档必须从内存中关闭。 这意味着不可见的客户端必须侦听 RDT 事件以跟踪此事件。 下次需要该文档时，必须重新打开该文档。
