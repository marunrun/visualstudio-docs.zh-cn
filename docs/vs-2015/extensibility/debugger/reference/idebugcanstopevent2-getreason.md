---
title: IDebugCanStopEvent2::GetReason |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191157"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取调试引擎 (DE) 是为什么想要停止的原因。  
  
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
 [out]返回一个值从[CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)介绍了此事件的原因的枚举。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法通常称为之前[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)方法，以便调用方可以确定是否将传递非零值 (`TRUE`) 到`IDebugCanStopEvent2::CanStop`方法。  
  
 正在停止的原因可以是`CANSTOP_ENTRYPOINT`，这意味着 DE 已达到的入口点，或`CANSTOP_STEPIN`，这意味着 DE 单步执行函数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)   
 [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)   
 [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
