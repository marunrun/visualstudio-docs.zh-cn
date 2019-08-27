---
title: 当断点绑定或解除绑定 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 003fd7a543e45c19fafbc19b306e58cc39a5e984
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348281"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>当断点绑定或解除绑定
不能在调用的时绑定断点时[IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)方法中，绑定时间，并创建的断点的时间不同。

## <a name="methods-called"></a>调用的方法
 会话调试管理器 (SDM) 调用以下方法：

1. [IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE 返回[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)。

2. [IDebugPendingBreakpoint2::Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。

3. [IDebugPendingBreakpoint2::Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)。

4. [IDebugPendingBreakpoint2::Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)方法并返回 S_OK。 DE 发送[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)或[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)。

5. [IDebugBreakpointBoundEvent2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)并[IDebugBreakpointBoundEvent2::EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)方法来验证并获取绑定的断点。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)