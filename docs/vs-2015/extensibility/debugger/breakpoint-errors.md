---
title: 断点错误 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e98dc5e4645ac67ecdf5ebb06ecf0f31510202e2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147979"
---
# <a name="breakpoint-errors"></a>断点错误
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

以下介绍的过程，当尝试绑定到代码断点，但失败：  
  
## <a name="troubleshooting-a-breakpoint-error"></a>断点错误进行故障排除  
  
1. 调试引擎 (DE) 将发送[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)会话调试管理器 (SDM)。  
  
2. SDM 调用[IDebugBreakpointErrorEvent2::GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2 * * `ppErrorBP`) 若要获取错误断点。  
  
3. SDM 调用[IDebugErrorBreakpoint2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)获取挂起断点错误断点的起源。  
  
4. SDM 调用[IDebugErrorBreakpoint2::GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)获取错误断点绑定失败的原因的原因。  
  
## <a name="see-also"></a>请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
