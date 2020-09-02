---
title: IDebugCanStopEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc4ac1f3a8d9b470fbb3734f822601a7dce08a44
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696674"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口用于向会话调试管理器 (SDM) 是否在当前代码位置停止。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugCanStopEvent2 : IUknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口以支持单步执行源代码。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问 `IDebugEvent2` 接口) 。  
  
 此接口的实现必须将 [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) 的 SDM 调用传达给调试引擎。 例如，可以使用发布到调试引擎消息处理线程的消息或实现此接口的对象保存对调试引擎的引用，并使用传入的标志回调到调试引擎 `IDebugCanStopEvent2::CanStop` 。  
  
## <a name="notes-for-callers"></a>调用方说明  
 每次请求取消时，DE 都可以发送此方法，而 DE 是单步执行代码。 此事件在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugCanStopEvent2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|获取此事件的原因。|  
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|指定正在调试的程序是否应在此事件 (位置停止，并发送一个描述停止) 的原因或只是继续执行的事件。|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|获取描述此事件位置的文档上下文。|  
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|获取描述此事件位置的代码上下文。|  
  
## <a name="remarks"></a>备注  
 如果用户执行步骤进入函数，并且没有在其中找到调试信息，或者存在调试信息，则 de 将发送此接口，但不知道是否可以为该位置显示源代码。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
