---
title: IDebugEngineProgram2：： WatchForExpressionEvaluationOnThread |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
helpviewer_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
ms.assetid: 01d05e77-8cac-4d1b-b19f-25756767ed27
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ebc513ead1ae911147217becd8f541cb11cd5585
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431467"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

允许 (或不允许) 表达式计算在给定线程上发生，即使程序已停止也是如此。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT WatchForExpressionEvaluationOnThread(   
   IDebugProgram2*       pOriginatingProgram,  
   DWORD                 dwTid,  
   DWORD                 dwEvalFlags,  
   IDebugEventCallback2* pExprCallback,  
   BOOL                  fWatch  
);  
```  
  
```csharp  
int WatchForExpressionEvaluationOnThread(   
   IDebugProgram2       pOriginatingProgram,  
   uint                  dwTid,  
   uint                  dwEvalFlags,  
   IDebugEventCallback2 pExprCallback,  
   int                   fWatch  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pOriginatingProgram`  
 中表示计算表达式的程序的 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象。  
  
 `dwTid`  
 中指定线程的标识符。  
  
 `dwEvalFlags`  
 中 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举中的标志的组合，该枚举指定如何执行计算。  
  
 `pExprCallback`  
 中用于发送在表达式计算过程中发生的调试事件的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。  
  
 `fWatch`  
 中如果 () 非零 `TRUE` ，则允许对由标识的线程进行表达式计算 `dwTid` ; 否则，零 (`FALSE`) 在该线程上不允许使用表达式计算。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 当会话调试管理器 (SDM) 请求由参数标识的程序时， `pOriginatingProgram` 它会通过调用此方法通知所有其他附加程序。  
  
 由于函数求值或对任何属性的计算，一个程序中的表达式计算可能会导致代码在其他程序中运行 `IDispatch` 。 因此，此方法允许表达式计算运行并完成，即使此程序中的线程可能已停止也是如此。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
