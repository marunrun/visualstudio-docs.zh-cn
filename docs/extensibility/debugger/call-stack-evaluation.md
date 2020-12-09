---
title: 调用堆栈计算 |Microsoft Docs
description: 了解 EnumFrameInfo 方法以及如何实现它以查看中断模式下调用堆栈的堆栈帧。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: fc637ff3ce2fe596eed48684523da7114fe0a03a
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914668"
---
# <a name="call-stack-evaluation"></a>调用堆栈计算
若要在中断模式下查看调用堆栈的堆栈帧，必须实现 [EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) 方法。

## <a name="methods-for-evaluation"></a>计算方法
 对于简单的调试引擎 (DE) ，可能只有一个堆栈帧。 若要在中断模式下检查堆栈帧，必须实现 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)的以下方法。

|方法|说明|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|获取堆栈帧的代码上下文。 代码上下文表示堆栈帧中的当前指令指针。|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|获取堆栈帧的文档上下文。 文档上下文表示堆栈帧在源代码中的当前位置。 在程序中停止时，需要查看源代码。|

 这些方法要求实现一些上下文相关的接口和方法。 因此，必须实现 [GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) 方法和 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md)的以下方法。

|方法|说明|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|获取文档上下文的文件语句范围。|

 若要枚举代码上下文，必须实现 [IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)的所有方法。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
