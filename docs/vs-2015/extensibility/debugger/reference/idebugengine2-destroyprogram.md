---
title: IDebugEngine2::DestroyProgram |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9faacd80b036282a088b006a15eb9500e8606c5e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196029"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

通知的调试引擎 (DE) 指定的程序已异常终止，DE 应清理对该程序的所有引用和发送程序销毁事件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT DestroyProgram(   
   IDebugProgram2* pProgram  
);  
```  
  
```cpp#  
int DestroyProgram(   
   IDebugProgram2 pProgram  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pProgram`  
 [in][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示已异常终止该程序。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法后，随后会发送 DE [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)回会话调试管理器 (SDM) 的事件。  
  
 未实现此方法 (返回`E_NOTIMPL`) 如果 DE 为正在调试的程序在同一进程中运行。 仅当 DE SDM 同一个进程中运行，实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
