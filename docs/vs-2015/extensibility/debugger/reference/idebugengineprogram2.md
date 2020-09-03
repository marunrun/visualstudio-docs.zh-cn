---
title: IDebugEngineProgram2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2c265cbfc89d0b637b1d2f37a3e3b9e948a8dd8f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687790"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供多线程调试支持。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEngineProgram2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎实现此接口以支持同时调试多个线程。 在实现 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的同一对象上实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 使用 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) 从接口获取此接口 `IDebugProgram2` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugEngineProgram2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|停止在此程序中运行的所有线程。|  
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|监视执行 (或停止监视执行) 在给定线程上发生。|  
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|允许 (或不允许) 表达式计算在给定线程上发生，即使程序已停止也是如此。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 将调用此接口以响应 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 事件，并设置 "监视线程步骤" 和 "在线程上监视表达式计算" 状态。 每当程序停止时调用[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md);此方法为程序提供了终止所有线程的机会。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
