---
title: 进入中断模式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c4251779593e237713258fd54c80dcb311ce4b80
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182249"
---
# <a name="entering-break-mode"></a>进入中断模式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

以下介绍单步执行函数，运行到源代码中，包含光标的行或运行到断点后遇到断点时，会发生的过程。  
  
## <a name="break-mode-process"></a>中断模式进程  
  
1. 调试引擎 (DE) 将发送[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)， [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)，或任何其他 stopping 事件会导致 IDE 以进入中断模式。  
  
2. SDM，如下所示获取从该线程的调用堆栈信息：  
  
    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)  
  
    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)  
  
    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)  
  
    - [IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)获取源代码信息  
  
    - [IDebugDocumentContext2::GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)若要获取文件名称  
  
    - [IDebugDocumentContext2::GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)可获取语句范围  
  
    - [IDebugStackFrame2::GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)获取内存信息  
  
## <a name="see-also"></a>请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
