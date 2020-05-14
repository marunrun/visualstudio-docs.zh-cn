---
title: 堆叠帧 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1ea79ad199e20afeb5d2bf1ca6a3cf881c6d51c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712846"
---
# <a name="stack-frames"></a>堆叠帧
在调试器体系结构中，*堆栈帧*：

- 是提供线程执行上下文的堆栈的抽象。 线程始终在函数中执行。 堆栈帧保存函数的局部变量及其参数。 为了使用 Visual Studio 进行调试，正在调试的语言或环境必须支持堆栈帧。

- 可以标识和描述自身，也可以返回关联的线程。 堆栈帧还可以返回表示当前指令指针以及关联的文档和表达式计算上下文的代码上下文。

- 具有描述局部变量和参数的名称、类型和值的属性，这些属性将显示在各种 IDE 调试窗口中。

- 由[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口表示，该接口通常由调试引擎 （DE） 或虚拟机创建，作为执行线程的结果。

## <a name="see-also"></a>请参阅
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
