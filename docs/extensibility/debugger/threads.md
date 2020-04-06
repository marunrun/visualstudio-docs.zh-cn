---
title: 线程 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8ed5c06e0c42dac1f0539cc2c7c5886d95b23ae1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712480"
---
# <a name="threads"></a>线程数
在调试器体系结构中，*线程*：

- 是计算的基本单位。 线程在单个调用堆栈的上下文中按顺序执行其指令，从一个代码上下文移动到下一个代码上下文。

- 可以标识自身及其正在运行的程序。 可以命名、挂起和恢复线程。 线程还可以枚举其关联的堆栈帧，在某些情况下，可以移动到另一个堆栈帧。 给定堆栈帧的上下文，线程可以返回其关联的逻辑线程（如果有）。 线程具有可在 IDE**的"线程"** 窗口中显示的属性（如挂起计数）。

- 由[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)接口表示，通常由调试引擎 （DE） 或虚拟机作为执行程序的结果创建。

## <a name="see-also"></a>请参阅
- [程序](../../extensibility/debugger/programs.md)
- [堆叠帧](../../extensibility/debugger/stack-frames.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
