---
title: 呼叫堆栈评估 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b5557d7eae0ffe54b0f01f1f9e95935d71455229
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739175"
---
# <a name="call-stack-evaluation"></a>调用堆栈评估
为了在中断模式下查看调用堆栈的堆栈帧，必须实现[EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)方法。

## <a name="methods-for-evaluation"></a>评价方法
 对于简单的调试引擎 （DE），可能只有一个堆栈帧。 要在中断模式下检查堆栈帧，必须实现[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)的以下方法。

|方法|描述|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|获取堆栈帧的代码上下文。 代码上下文表示堆栈框架中的当前指令指针。|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|获取堆栈框架的文档上下文。 文档上下文表示堆栈帧的源代码中的当前位置。 在程序中停止时查看源代码所需的。|

 这些方法需要实现多个与上下文相关的接口和方法。 因此，您必须实现[GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)方法和[IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md)的以下方法。

|方法|描述|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|获取文档上下文的文件语句范围。|

 要枚举代码上下文，必须实现[IEnumDebugCodeContext2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)的所有方法。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
