---
title: IDebugStopCompleteEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
ms.assetid: ff3e89f4-61bb-489d-901c-447260100218
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9c2a6a6e69bf47751706710801dd78c832ccd2c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62546911"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

当程序停止时，调试引擎 (DE) 可以将此可选事件发送到会话调试管理器 (SDM) 。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugStopCompleteEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 这是的新接口 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 。 以前的版本不支持异步停止。  
  
 在多进程或多程序方案中，由 SDM 调用[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)。 当一个程序向 SDM 发送停止事件时，SDM 还请求其他程序停止。  
  
 它用于异步通知 SDM 程序已停止。 这对于解释器调试引擎非常有用，在这种情况下，调试程序中有时不会运行任何代码，因此无法同步完成 [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) 。 如果调试引擎要使用此异步通知，则它必须 `S_ASYNC_STOP` 从 [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)返回。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
