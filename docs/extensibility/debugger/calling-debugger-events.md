---
title: 调用调试器事件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 869bd87952aebf8ad640c5aeb439c9e99929f4c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739163"
---
# <a name="call-debugger-events"></a>调用调试器事件
调试会话中的事件按特定顺序发生。

## <a name="discussion"></a>讨论区
 要了解调试引擎 （DE） 和会话调试管理器 （SDM） 之间的调用模式，以下表示典型调试会话中发生的事件的调用顺序：

1. [附加和分离到程序](../../extensibility/debugger/attaching-and-detaching-to-a-program.md)

2. [启动调试器](../../extensibility/debugger/launching-the-debugger.md)

3. [终止程序](../../extensibility/debugger/terminating-a-program.md)

4. [创建断点](../../extensibility/debugger/creating-a-breakpoint.md)

5. [当断点绑定或变为未绑定时](../../extensibility/debugger/when-a-breakpoint-binds-or-becomes-unbound.md)

6. [断点错误](../../extensibility/debugger/breakpoint-errors.md)

7. [命中断点](../../extensibility/debugger/hitting-a-breakpoint.md)

8. [删除断点](../../extensibility/debugger/deleting-a-breakpoint.md)

9. [进入中断模式](../../extensibility/debugger/entering-break-mode.md)

10. [步进进入中断模式](../../extensibility/debugger/stepping-in-break-mode.md)

11. [中断模式下的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

12. [异常处理](../../extensibility/debugger/exception-handling-visual-studio-sdk.md)

## <a name="see-also"></a>请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
