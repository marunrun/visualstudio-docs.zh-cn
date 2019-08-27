---
title: 当断点绑定或解除绑定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1425edc2c8fc3fe8c38c133388f90b18b516b09
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162168"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>断点绑定或解除绑定时
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

不能在调用的时绑定断点时[IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)方法中，绑定时间，并创建的断点的时间不同。  
  
## <a name="methods-called"></a>调用的方法  
 会话调试管理器 (SDM) 调用以下方法：  
  
1. [IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE 返回[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)。  
  
2. [IDebugPendingBreakpoint2::Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。  
  
3. [IDebugPendingBreakpoint2::Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)。  
  
4. [IDebugPendingBreakpoint2::Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)方法并返回 S_OK。 DE 发送[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)或[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)。  
  
5. [IDebugBreakpointBoundEvent2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)并[IDebugBreakpointBoundEvent2::EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)方法来验证并获取绑定的断点。  
  
## <a name="see-also"></a>请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
