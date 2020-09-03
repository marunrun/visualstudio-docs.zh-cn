---
title: 程序控制 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e77e233050c5ce10aef5053f82c8d26cb984b85
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738226"
---
# <a name="program-control"></a>程序控制
在 Visual Studio 调试中，以下所有单步执行和继续例程都在程序级别进行：

- 设置下一条语句，即将计算机设置为在特定帧环境下执行的下一条指令

- 正在执行，即继续退出单步执行模式

- 单步执行下一条指令

- 继续当前步进模式

- 挂起程序包含的线程

- 恢复程序包含的线程

> [!NOTE]
> 查看调用堆栈是在线程级别实现的。 若要在查看线程的调用堆栈时枚举帧信息，必须实现 [IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md) 接口的所有方法。

## <a name="methods-of-program-control"></a>程序控制方法
 下表显示了 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 的方法，这些方法必须为最低功能调试引擎实现 (DE) 和执行控制。

|方法|说明|
|------------|-----------------|
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|继续从停止状态运行程序包含的所有线程。 对于执行控制是必需的。|
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|继续从停止状态运行程序包含的所有线程。 对于执行控制是必需的。|
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|在给定线程上执行步骤。 继续运行程序包含的所有其他线程。 对于执行控制是必需的。|

 对于多线程程序，还必须实现 [IDebugProgram2：： EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) 方法和 [IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md) 接口的所有方法。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
