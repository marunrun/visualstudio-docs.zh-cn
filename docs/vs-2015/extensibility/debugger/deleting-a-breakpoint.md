---
title: 删除断点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42cd353c216c21d14c4f6592da809c72acdba664
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840562"
---
# <a name="deleting-a-breakpoint"></a>删除断点
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下面描述了删除挂起断点时的过程：  
  
## <a name="deletion-process"></a>删除过程  
 会话调试管理器 (SDM) 调用 [IDebugPendingBreakpoint2：:D e) ](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) 方法来删除挂起的断点以及从该断点绑定的所有绑定断点。  
  
> [!NOTE]
> 还可以通过调用 [IDebugBoundBreakpoint2：:D e) ](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)删除单个绑定断点。  
  
## <a name="see-also"></a>另请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
