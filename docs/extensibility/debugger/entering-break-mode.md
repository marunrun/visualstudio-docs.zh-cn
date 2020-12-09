---
title: 进入中断模式 |Microsoft Docs
description: 了解在函数中遇到的断点、运行到光标处的源代码行或运行到断点时所发生的过程。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: e73c64d17aee48cdb67a110e93aa556f112a1014
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915227"
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

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
