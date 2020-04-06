---
title: 击中断点 |微软文档
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
ms.openlocfilehash: 6e75eb1e807e72f3bd035b5dd0534860f5fd8df2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738568"
---
# <a name="hit-a-breakpoint"></a>命中断点
以下部分介绍调试引擎 （DE） 在运行或步进时遇到断点的过程：

## <a name="troubleshoot-a-hit-breakpoint"></a>排除命中断点故障

1. DE 将[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)接口作为**EVENT_SYNC_STOP**发送。

2. 会话调试管理器 （SDM） 调用[IDebugBreakpointEvent2：：：enumBreakpoint](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md)获取命中的断点。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
