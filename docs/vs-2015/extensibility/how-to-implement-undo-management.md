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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840770"
---
# <a name="how-to-implement-undo-management"></a>如何：实现撤消管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用于撤消管理的主接口是 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> 由环境实现的。 若要支持撤消管理，请实现单独的撤消单元 (即， <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> 其中可包含多个单独的步骤。  
  
 如何实现撤消管理取决于编辑器是否支持多个视图。 以下各节详细介绍了每种实现的过程。  
  
## <a name="cases-where-an-editor-supports-a-single-view"></a>编辑器支持单个视图的情况  
 在这种情况下，编辑器不支持多个视图。 只有一个编辑器和一个文档，它们支持 "撤消"。 使用以下过程来实现撤消管理。  
  
#### <a name="to-support-undo-management-for-a-single-view-editor"></a>支持单一视图编辑器的撤消管理  
  
1. 对的 `QueryInterface` `IServiceProvider` 窗口框架上的接口调用 `IOleUndoManager` ，从文档视图对象访问撤消管理器 (`IID_IOLEUndoManager`) 。  
  
2. 当视图被放置到窗口框架中时，它将获取一个可用于调用的站点指针 `QueryInterface` `IServiceProvider` 。  
  
## <a name="cases-where-an-editor-supports-multiple-views"></a>编辑器支持多个视图的情况  
 如果你有文档和视图分离，则通常会有一个与文档自身关联的撤消管理器。 所有撤消单元都放置在与文档数据对象相关联的一个撤消管理器中。  
  
 文档数据对象将调用 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 来实例化撤消管理器（指定 CLSID_OLEUndoManager 的类标识符），而不是查询撤消管理器的视图。 在 OCUNDOID 文件中定义类标识符。  
  
 使用 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 创建自己的撤消管理器实例时，请使用以下过程将撤消管理器挂钩到环境中。  
  
#### <a name="to-hook-your-undo-manager-into-the-environment"></a>将撤消管理器挂钩到环境中  
  
1. 对 `QueryInterface` 返回的对象调用 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> `IID_IOleUndoManager` 。 将指针存储到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> 。  
  
2. 对 `QueryInterface` `IOleUndoManager` 的调用 `IID_IOleCommandTarget` 。 将指针存储到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。  
  
3. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 将和调入到存储 `IOleCommandTarget` 接口，以获取以下 StandardCommandSet97 命令：  
  
   - cmdidUndo  
  
   - cmdidMultiLevelUndo  
  
   - cmdidRedo  
  
   - cmdidMultiLevelRedo  
  
   - cmdidMultiLevelUndoList  
  
   - cmdidMultiLevelRedoList  
  
4. 对 `QueryInterface` `IOleUndoManager` 的调用 `IID_IVsChangeTrackingUndoManager` 。 将指针存储到 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager> 。  
  
    使用指向的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager> 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.MarkCleanState%2A> 、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.AdviseTrackingClient%2A> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.UnadviseTrackingClient%2A> 方法。  
  
5. 对 `QueryInterface` `IOleUndoManager` 的调用 `IID_IVsLinkCapableUndoManager` 。  
  
6. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkCapableUndoManager.AdviseLinkedUndoClient%2A> 你的文档，该文档还应实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoClient> 接口。 关闭文档后，调用 `IVsLinkCapableUndoManager::UnadviseLinkedUndoClient` 。  
  
7. 关闭文档后，请 `QueryInterface` 在撤消管理器中调用 `IID_IVsLifetimeControlledObject` 。  
  
8. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject.SeverReferencesToOwner%2A>。  
  
9. 当对文档进行了更改时，请 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> 使用类对管理器调用 `OleUndoUnit` 。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A>方法保留对对象的引用，因此通常会在之后立即将其释放 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> 。  
  
   `OleUndoManager`类表示单个撤消堆栈实例。 因此，对于每个要跟踪的数据实体，都有一个撤消管理器对象用于撤消或重做。  
  
> [!NOTE]
> 尽管 "撤消管理器" 对象由文本编辑器广泛使用，但它是一个不提供对文本编辑器的特定支持的常规组件。 如果要支持多层撤消或重做，可以使用此对象执行此操作。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject>   
 [如何：清除撤消堆栈](../extensibility/how-to-clear-the-undo-stack.md)
