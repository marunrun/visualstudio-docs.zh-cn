---
title: IDebugEngineProgram2 | Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687790"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供了多线程调试支持。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEngineProgram2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎实现此接口以支持多个线程的同时进行调试。 此接口上实现的相同对象实现[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)若要获取此接口从`IDebugProgram2`接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugEngineProgram2`。  
  
|方法|描述|  
|------------|-----------------|  
|[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|停止此程序中正在运行的所有线程。|  
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|执行 （或停止执行监视） 监视是否在给定的线程上发生。|  
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|允许 （或不允许） 表达式计算，即使程序已停止，在给定的线程上发生。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 会调用此接口以响应[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件并设置该程序的"监视的线程步骤"和"监视的表达式求值在线程"状态。 [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)每当调用程序是要停止; 此方法使程序终止所有线程。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
