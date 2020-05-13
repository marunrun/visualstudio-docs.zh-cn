---
title: 执行控制和状态评估 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc76ae97e8baa6ce78dd4d565109d6a19e2051e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738751"
---
# <a name="execution-control-and-state-evaluation"></a>执行控制和状态评估
调试应用程序需要实现诸如步进函数、在断点停止和继续执行等执行控制功能。 Visual Studio 调试基于调试器组件之间发送的事件，其执行控制。

## <a name="in-this-section"></a>在本节中
 [程序控制](../../extensibility/debugger/program-control.md)列出了在程序级别发生的以下例程：设置下一个语句、执行、步进、继续、挂起和恢复。

 [与断点相关的方法](../../extensibility/debugger/breakpoint-related-methods.md)定义 Visual Studio 支持的绑定和挂起的断点类型。

 [调用堆栈评估](../../extensibility/debugger/call-stack-evaluation.md)讨论允许在中断模式下查看调用堆栈堆栈帧的方法的实现。

 [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)说明调试引擎 （DE）、表达式计算 （EE） 和会话调试管理器如何参与对输入到 IDE 窗口之一的表达式的解析和评估。

 [控制事件](../../extensibility/debugger/control-events.md)讨论用于在程序受控执行期间发送事件的接口。
