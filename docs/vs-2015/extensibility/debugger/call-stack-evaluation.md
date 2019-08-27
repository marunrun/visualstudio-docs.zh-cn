---
title: 调用堆栈计算 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 15fecbc61fec8ba7aa62ca7d79cf11c56b7ce938
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68146406"
---
# <a name="call-stack-evaluation"></a>调用堆栈计算
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要在中断模式下查看调用堆栈的堆栈帧，则必须实现[EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)方法。  
  
## <a name="methods-for-evaluation"></a>用于评估方法  
 对于简单的调试引擎 (DE)，可能只有一个堆栈帧。 若要检查的堆栈帧在中断模式下，必须实现的以下方法[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)。  
  
|方法|描述|  
|------------|-----------------|  
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|获取一个堆栈帧的代码上下文。 代码上下文表示堆栈帧中的当前指令指针。|  
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|获取一个堆栈帧的文档上下文。 文档上下文表示当前堆栈帧的源代码中的位置。 所需的程序中停止时查看的源代码。|  
  
 这些方法需要一些上下文相关接口和方法的实现。 因此，必须实现[GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)方法，下列方法之一[IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md)。  
  
|方法|描述|  
|------------|-----------------|  
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|获取文件语句范围的文档上下文。|  
  
 若要枚举的代码上下文，必须实现的所有方法[IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)。  
  
## <a name="see-also"></a>请参阅  
 [执行控件和状态计算](../../extensibility/debugger/execution-control-and-state-evaluation.md)
