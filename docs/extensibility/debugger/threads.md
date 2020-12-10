---
title: 线程 |Microsoft Docs
description: 本文介绍 Visual Studio 的调试器结构中的线程定义和角色。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: b259ffd7814b42145489ee5990cee6da891a9d10
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995949"
---
# <a name="threads"></a>线程
调试程序体系结构中的 *线程*：

- 是计算的基本单位。 线程按顺序在单个调用堆栈的上下文中执行其说明，并从一个代码上下文移到下一个调用堆栈。

- 可以标识自身及其正在运行的程序。 可以命名、挂起和恢复线程。 线程还可以枚举其关联的堆栈帧，并且在某些情况下，可以将其移动到另一个堆栈帧。 给定堆栈帧的上下文，线程可以返回其关联的逻辑线程（如果有）。 线程具有可在 IDE 的 " **线程** " 窗口中显示的属性，例如挂起计数。

- 由 [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) 接口表示，此接口通常由调试引擎创建 (取消) 或虚拟机作为执行程序的结果。

## <a name="see-also"></a>另请参阅
- Programs 
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
