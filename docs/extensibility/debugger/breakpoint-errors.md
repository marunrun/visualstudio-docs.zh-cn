---
title: 断点错误 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31eabde4ae19ae7342188a5d2a16374b9c94afc0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332547"
---
# <a name="breakpoint-errors"></a>断点错误
以下介绍的过程，当尝试绑定到代码断点，但会失败。

## <a name="troubleshoot-a-breakpoint-error"></a>断点错误进行故障排除

1. 调试引擎 (DE) 将发送[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)会话调试管理器 (SDM)。

2. SDM 调用[IDebugBreakpointErrorEvent2::GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2 * * `ppErrorBP`) 若要获取错误断点。

3. SDM 调用[IDebugErrorBreakpoint2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)获取挂起断点错误断点的起源。

4. SDM 调用[IDebugErrorBreakpoint2::GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)获取错误断点绑定失败的原因的原因。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)