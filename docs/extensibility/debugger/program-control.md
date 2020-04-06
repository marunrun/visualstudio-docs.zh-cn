---
title: 程序控制 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738226"
---
# <a name="program-control"></a>程序控制
在 Visual Studio 调试中，以下所有步进和持续例程都发生在程序级别：

- 设置下一个语句，即将计算机设置为要在特定帧环境中执行的下一个指令

- 执行，即继续退出步进模式

- 步进下一个指令

- 继续当前步进模式

- 挂起程序中包含的线程

- 恢复程序中包含的线程

> [!NOTE]
> 查看调用堆栈是在线程级别实现的。 要枚举线程的调用堆栈时枚举帧信息，必须实现[IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md)接口的所有方法。

## <a name="methods-of-program-control"></a>程序控制方法
 下表显示了为最小功能调试引擎 （DE） 和执行控制而必须实现的[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)方法。

|方法|描述|
|------------|-----------------|
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|继续运行程序从停止状态包含的所有线程。 执行控制所需的。|
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|继续运行程序从停止状态包含的所有线程。 执行控制所需的。|
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|在给定的线程上执行步骤。 继续运行程序包含的所有其他线程。 执行控制所需的。|

 对于多线程程序，还必须实现[IDebugProgram2：：：enumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)方法以及[IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md)接口的所有方法。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
