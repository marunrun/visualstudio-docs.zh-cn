---
title: 如何：使用链接的撤消管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - linked undo management
ms.assetid: af5cc22a-c9cf-45b1-a894-1022d563f3ca
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 67d0d173909b8cdfe2eaf0d56aa5c99c437d5ad8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840456"
---
# <a name="how-to-use-linked-undo-management"></a>如何：使用链接的撤消管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过链接撤消，用户可以在多个文件中同时撤消相同的编辑。 例如，多个程序文件中的同步文本更改，如标头文件和 Visual C++ 文件，是链接的撤消事务。 链接撤消功能内置于环境的撤消管理器实现中，并 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> 使您可以操作此功能。 链接撤消是通过父撤消单元实现的，可以将单独的撤消堆栈链接在一起，以将其视为单个撤消单元。 下一节中详细介绍了如何使用链接撤消。  
  
### <a name="to-use-linked-undo"></a>使用链接的撤消  
  
1. 调用 `QueryService` `SVsLinkedUndoManager` 以获取指向的指针 `IVsLinkedUndoTransactionManager` 。  
  
2. 通过调用创建初始父链接的撤消单元 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager.OpenLinkedUndo%2A> 。 这会将一组撤消堆栈的起始点设置为组合到链接的撤消堆栈中。 在 `OpenLinkedUndo` 方法中，您还需要指定是否希望将链接的撤消为严格或非严格。 非严格链接的撤消行为意味着某些具有链接的撤消同级的文档可以关闭，并且仍会将其他链接的撤消同级置于其堆栈上。 严格链接的撤消行为指定所有链接的撤消同级堆栈必须一起撤消或全部撤消。 通过调用 [IOleUndoManager：： add](/windows/desktop/api/ocidl/nf-ocidl-ioleundomanager-add) 方法添加后续链接的撤消堆栈。  
  
3. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager.CloseLinkedUndo%2A> 以将所有链接的撤消单元回滚为一个。  
  
    > [!NOTE]
    > 若要在编辑器中实现链接的撤消管理，请添加撤消管理。 有关实现链接的撤消管理的详细信息，请参阅 [如何：实现撤消管理](../extensibility/how-to-implement-undo-management.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>   
 [IOleParentUndoUnit](/windows/desktop/api/ocidl/nn-ocidl-ioleparentundounit)   
 [IOleUndoUnit](/windows/desktop/api/ocidl/nn-ocidl-ioleundounit)   
 [如何：实现撤消管理](../extensibility/how-to-implement-undo-management.md)
