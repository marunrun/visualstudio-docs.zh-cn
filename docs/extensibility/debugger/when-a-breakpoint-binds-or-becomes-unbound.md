---
title: 当断点绑定或变为未绑定时 |Microsoft Docs
description: 了解未绑定断点。 如果在调用时无法绑定断点，则断点的绑定时间和创建时间不同。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: a48bd7ff011b6e8de6e9321a00b6bc20d54f0f0b
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995910"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>当断点绑定或变为未绑定断点时
当对 [IDebugPendingBreakpoint2：： CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md) 方法进行调用时，如果无法绑定断点，则断点的绑定时间和创建时间不同。

## <a name="methods-called"></a>调用的方法
 会话调试管理器 (SDM) 调用以下方法：

1. [IDebugEngine2：： CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE 返回一个 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)。

2. [IDebugPendingBreakpoint2：： Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。

3. [IDebugPendingBreakpoint2：：虚拟化](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)。

4. [IDebugPendingBreakpoint2：： Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)方法并返回 S_OK。 DE 发送 [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) 或 [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)。

5. [IDebugBreakpointBoundEvent2：： GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) 和 [IDebugBreakpointBoundEvent2：： EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) 方法，用于验证和获取绑定断点。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
