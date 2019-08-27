---
title: 如何：实现撤消管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 1942245d-7a1d-4a11-b5e7-a3fe29f11c0b
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f3d56ae02718f5dfdf373eeeb6aff774d11931e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435956"
---
# <a name="how-to-implement-undo-management"></a>如何：实现撤消管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用于撤消管理的主界面是<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>，这由环境实现。 若要支持撤消管理，实现单独的撤消单元 (即， <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit>，其中包含多个单独的步骤。  
  
 如何实现撤消管理根据您的编辑器是否支持多个视图，或不可能有所不同。 以下各节将详细的过程的每个实现。  
  
## <a name="cases-where-an-editor-supports-a-single-view"></a>其中一个编辑器支持单个视图的情况下  
 在此方案中，编辑器不支持多个视图。 只有一个编辑器和一个文档，并且它们支持撤消。 使用以下过程来实现撤消管理。  
  
#### <a name="to-support-undo-management-for-a-single-view-editor"></a>若要为单一视图编辑器支持撤消管理  
  
1. 调用`QueryInterface`上`IServiceProvider`接口上的窗口框架`IOleUndoManager`，从要访问撤消管理器的文档视图对象 (`IID_IOLEUndoManager`)。  
  
2. 当视图被放置到窗口框架后时，它将获取的站点指针，它可用于调用`QueryInterface`为`IServiceProvider`。  
  
## <a name="cases-where-an-editor-supports-multiple-views"></a>其中一个编辑器支持多个视图的情况下  
 如果必须文档和视图之间的分离，则通常一个撤消管理器与文档本身相关联。 所有的撤消单元将放置在与文档数据对象关联的一个撤消管理器。  
  
 而不是撤消管理器，其中还有一个为每个视图，视图查询的文档数据对象调用<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>实例化撤消管理器，并指定 CLSID_OLEUndoManager 类标识符。 OCUNDOID.h 文件中定义的类标识符。  
  
 当使用<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>创建撤消管理器实例，使用以下过程来挂接到环境的撤消管理器。  
  
#### <a name="to-hook-your-undo-manager-into-the-environment"></a>若要将撤消管理器挂钩到环境  
  
1. 调用`QueryInterface`从返回的对象上<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2>为`IID_IOleUndoManager`。 存储指向<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>。  
  
2. 调用`QueryInterface`上`IOleUndoManager`为`IID_IOleCommandTarget`。 存储指向<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。  
  
3. 中继你<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>并<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>调入存储`IOleCommandTarget`以下 StandardCommandSet97 命令的接口：  
  
   - cmdidUndo  
  
   - cmdidMultiLevelUndo  
  
   - cmdidRedo  
  
   - cmdidMultiLevelRedo  
  
   - cmdidMultiLevelUndoList  
  
   - cmdidMultiLevelRedoList  
  
4. 调用`QueryInterface`上`IOleUndoManager`为`IID_IVsChangeTrackingUndoManager`。 存储指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>。  
  
    使用指向指针<xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>来调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.MarkCleanState%2A>，则<xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.AdviseTrackingClient%2A>，和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.UnadviseTrackingClient%2A>方法。  
  
5. 调用`QueryInterface`上`IOleUndoManager`为`IID_IVsLinkCapableUndoManager`。  
  
6. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkCapableUndoManager.AdviseLinkedUndoClient%2A>您的文档，其中应实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoClient>接口。 关闭文档后，调用`IVsLinkCapableUndoManager::UnadviseLinkedUndoClient`。  
  
7. 关闭文档后，调用`QueryInterface`上为你撤消管理器`IID_IVsLifetimeControlledObject`。  
  
8. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject.SeverReferencesToOwner%2A>。  
  
9. 当对文档进行更改时，调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A>上的管理器`OleUndoUnit`类。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A>方法中保留引用对象，因此通常在发布紧靠其后<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A>。  
  
   `OleUndoManager`类表示单个撤消堆栈实例。 因此，是每个被跟踪的撤消或重复的数据实体的一个撤消管理器对象。  
  
> [!NOTE]
> 文本编辑器中广泛使用的撤消管理器对象，它是文本编辑器中没有特定支持的通用组件。 如果你想要支持多级撤消或重做，可以使用此对象来执行此操作。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject>   
 [如何：清除撤消堆栈](../extensibility/how-to-clear-the-undo-stack.md)
