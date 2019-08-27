---
title: IDebugExceptionEvent2::PassToDebuggee |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150399"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定异常应传递到时恢复执行，正在调试的程序还是应放弃该异常。  
  
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
  
#### <a name="parameters"></a>Parameters  
 `fPass`  
 [in]非零值 (`TRUE`) 如果异常应传递到时恢复执行，正在调试的程序或零 (`FALSE`) 如果应放弃该异常。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法不会实际导致要在正在调试的程序中执行的任何代码。 在调用是只是设置下一步执行代码的状态。 例如，调用[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)方法可能会返回`S_OK`与[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)。`dwState` 字段设置为`EXCEPTION_STOP_SECOND_CHANCE`。  
  
 IDE 可能会收到[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)事件，并调用[继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)方法。 调试引擎 (DE) 应具有一个默认行为来处理如果`PassToDebuggee`不会调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)   
 [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)   
 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
