---
title: IDebugExceptionEvent2：:P assToDebuggee |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ecc7eb3830522cdee0022f4193482daab3780230
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150399"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定是否应在执行恢复时将异常传递给正在调试的程序，或是否应丢弃异常。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT PassToDebuggee(  
   BOOL fPass  
);  
```  
  
```csharp  
int PassToDebuggee(  
   int fPass  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fPass`  
 中 `TRUE` 如果异常应传递到执行恢复时正在调试的程序，则为非零 () 如果应丢弃异常，则为零 (`FALSE`) 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法实际上不会导致在正在调试的程序中执行任何代码。 调用只是为下一个代码执行设置状态。 例如，对 [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) 方法的调用可能会返回 `S_OK` [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)。`dwState` 字段设置为 `EXCEPTION_STOP_SECOND_CHANCE` 。  
  
 IDE 可能会收到 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) 事件并调用 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) 方法。 如果未调用方法，调试引擎 (DE) 应具有处理事例的默认行为 `PassToDebuggee` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)   
 [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)   
 [继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
