---
title: IDebugCanStopEvent2：： GetReason |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 707488abed004adaa75c84f16358bdd8a979eb71
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191157"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取调试引擎 (DE) 要停止的原因。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetReason(   
   CANSTOP_REASON* pcr  
);  
```  
  
```csharp  
int GetReason(   
   out enum_CANSTOP_REASON pcr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pcr`  
 弄返回 [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md) 枚举中的一个值，该值描述此事件的原因。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 通常在 [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) 方法之前调用此方法，以便调用方能够确定是否将非零 () 传递 `TRUE` 给 `IDebugCanStopEvent2::CanStop` 方法。  
  
 停止的原因可能是 `CANSTOP_ENTRYPOINT` ，这意味着取消了某个入口点或 `CANSTOP_STEPIN` ，这意味着 de 进入了一个函数。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)   
 [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)   
 [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
