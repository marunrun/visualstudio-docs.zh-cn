---
title: 命中断点 |Microsoft Docs
description: 本文介绍当调试引擎在运行或单步执行时命中断点时所发生的过程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc796689b56518948c62196407ddeaefe3ea822f
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560845"
---
# <a name="hit-a-breakpoint"></a>命中断点
以下部分介绍当调试引擎 (在运行或单步执行时) 命中断点时的进程：

## <a name="troubleshoot-a-hit-breakpoint"></a>命中断点的疑难解答

1. DE 发送 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) 接口作为 **EVENT_SYNC_STOP**。

2. 会话调试管理器 (SDM) 调用 [IDebugBreakpointEvent2：：： EnumBreakpoints](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) 以获取命中的断点。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
