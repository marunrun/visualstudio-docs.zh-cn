---
title: 当断点绑定或变为未绑定 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3253841778fe5a07e00b644423495b8ceee1a335
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712336"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>当断点绑定或变为未绑定时
当在对[IDebugPendingBreakpoint2：：CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)方法进行调用时无法绑定断点时，断点的绑定时间和创建时间是不同的。

## <a name="methods-called"></a>调用的方法
 会话调试管理器 （SDM） 调用以下方法：

1. [IDebugEngine2：：创建挂起的断点](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE 返回一个[IDebug 挂起的断点2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)。

2. [IDebug 挂起断点2：：启用](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。

3. [IDebug 挂起断点2：：虚拟化](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)。

4. [IDebugPendingBreakpoint2：：绑定](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)方法并返回S_OK。 DE 发送[IDebugBreakpoint 绑定事件2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)或[IDebugBreakpoint错误事件2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)。

5. [IDebugBreakpoint绑定事件2：：获取待定断点](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)和[IDebugBreakpoint绑定事件2：：enumBoundBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)方法以验证和获取绑定的断点。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
