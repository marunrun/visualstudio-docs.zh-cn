---
title: 进入中断模式 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4bbcec8adf6468f70d95df5f291ce1e5540406cf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738877"
---
# <a name="enter-break-mode"></a>进入中断模式
以下信息描述了单步执行函数后遇到断点、运行到包含游标的源代码行或运行到断点时所发生的过程。

## <a name="break-mode-process"></a>中断模式进程

1. 调试引擎 (DE) 发送 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)、 [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)或任何其他停止事件，使 IDE 进入中断模式。

2. SDM 从线程获取调用堆栈信息，如下所示：

    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)

    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)

    - [IDebugStackFrame2：： GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) 获取源代码信息

    - [IDebugDocumentContext2：： GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md) 获取文件名

    - [IDebugDocumentContext2：： GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) 获取语句范围

    - [IDebugStackFrame2：： GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md) 获取内存信息

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
