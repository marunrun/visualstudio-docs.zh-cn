---
title: 断点错误 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0766792f19faf7c1933c6576ab41f65ec1b31ae9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739215"
---
# <a name="breakpoint-errors"></a>断点错误
当断点尝试绑定到代码但失败时，下面描述了该过程。

## <a name="troubleshoot-a-breakpoint-error"></a>排除断点错误

1. 调试引擎 （DE） 向会话调试管理器 （SDM） 发送[IDebugBreakpointErrorEvent2。](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)

2. SDM 调用[IDebugBreakpointErrorEvent2：：获取错误断点](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)（IDebugErrorBreakpoint2+）`ppErrorBP`以获取错误断点。

3. SDM 调用[IDebugError 断点2：：获取待定断点](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)以获取错误断点源自的挂起断点。

4. SDM 调用[IDebugErrorBreakpoint2：：获取断点解析](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)，以获取有关错误断点未能绑定的原因。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
