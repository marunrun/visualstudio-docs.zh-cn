---
title: 线程 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e9759536e1b27018a3361bbb723b4cde0f88269e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333662"
---
# <a name="threads"></a>线程
在调试器体系结构中，*线程*:

- 是计算的基本单位。 线程按顺序执行其上下文中的单一调用堆栈，将从一种代码上下文移到下一步的说明。

- 可以标识本身和在运行的程序。 可以命名、 挂起，但恢复线程。 线程还可以枚举其关联的堆栈帧，并在某些情况下可以移动到另一个堆栈帧。 给定堆栈帧上下文内的，线程可以返回其关联的逻辑线程，如果有的话。 线程具有属性，例如挂起计数，在中显示**线程**在 IDE 的窗口。

- 为由[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)接口，通常创建的调试引擎 (DE) 或虚拟机，因此执行程序。

## <a name="see-also"></a>请参阅
- [程序](../../extensibility/debugger/programs.md)
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)