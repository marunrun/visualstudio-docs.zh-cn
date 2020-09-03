---
title: IDebugProgram3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ae6de25108cf93314db17a2ac8de9ce8b1dcaed2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148610"
---
# <a name="idebugprogram3"></a>IDebugProgram3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示在进程中运行的程序，并通过提供线程信息来扩展 [执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md) 。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgram3 : IDebugProgram3  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) ，自定义端口供应商实现此接口来表示进程中的程序。 会话调试管理器 (SDM) 还实现此接口以提供要 [附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)的信息。  
  
## <a name="notes-for-callers"></a>调用方说明  
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件将为新程序返回此接口。 此接口还可用作多个接口上许多方法的参数。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugProgram3` 。  
  
|方法|说明|  
|------------|-----------------|  
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|执行程序。 返回线程，以向调试器显示用户在执行时查看的线程的信息。|  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="remarks"></a>备注  
 程序是在特定运行时结构中运行的线程容器，而进程由一个或多个程序组成。  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)   
 [一个](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)   
 [引发](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [附件](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)   
 [引发](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
