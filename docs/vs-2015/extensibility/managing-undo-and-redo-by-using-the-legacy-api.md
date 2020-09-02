---
title: 使用旧版 API 管理撤消和重做 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 838c0ddf-fdf3-4df1-8d21-79610b8ba0b1
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7c2133c75b32e56c1a054740bd829bd04cac97cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194359"
---
# <a name="managing-undo-and-redo-by-using-the-legacy-api"></a>使用旧版 API 管理撤消和恢复
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器必须支持撤消操作，使用户可以在修改代码时撤消最近的更改。 在和下实现的大多数编辑器都 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 可以通过集成开发环境自动提供撤消支持 (IDE) 。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：实现撤消管理](../extensibility/how-to-implement-undo-management.md)  
 为具有单个或多个视图的编辑器提供撤消功能。  
  
 [如何：清除撤消堆栈](../extensibility/how-to-clear-the-undo-stack.md)  
 介绍如何清除撤消堆栈。  
  
 [如何：使用链接的撤消管理](../extensibility/how-to-use-linked-undo-management.md)  
 将链接的撤消管理合并到编辑器中。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>  
 为支持多个视图的编辑器提供撤消管理。  
  
## <a name="related-sections"></a>相关章节
