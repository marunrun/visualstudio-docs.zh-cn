---
title: 管理撤消和重做通过旧版 API |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194359"
---
# <a name="managing-undo-and-redo-by-using-the-legacy-api"></a>使用旧版 API 管理撤消和恢复
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器必须支持撤消操作，可让用户反转其最新更改时它们修改代码。 在实现大多数编辑器[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]和[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]可以撤消支持自动提供的集成的开发环境 (IDE)。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：实现撤消管理](../extensibility/how-to-implement-undo-management.md)  
 使用单个或多个视图的编辑器提供恢复数据的功能。  
  
 [如何：清除撤消堆栈](../extensibility/how-to-clear-the-undo-stack.md)  
 说明如何清除撤消堆栈。  
  
 [如何：使用链接的撤消管理](../extensibility/how-to-use-linked-undo-management.md)  
 将链接的撤消管理合并到您的编辑器。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>  
 提供支持多个视图的编辑器的撤消管理。  
  
## <a name="related-sections"></a>相关章节
