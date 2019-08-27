---
title: IDebugProgram2::Attach |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::Attach
helpviewer_keywords:
- IDebugProgram2::Attach
ms.assetid: de069fbf-a565-4905-b102-f5658c55aacd
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0e029c2e16d5eee1764b463b21fc0fd8a4032252
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62580399"
---
# <a name="idebugprogram2attach"></a>IDebugProgram2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将附加到该程序。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Attach(   
   IDebugEventCallback2* pCallback  
);  
```  
  
```csharp  
int Attach(   
   IDebugEventCallback2 pCallback  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pCallback`  
 [in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)用于调试事件通知对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了一些可能的错误代码。  
  
|“值”|描述|  
|-----------|-----------------|  
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的程序已附加到调试器。|  
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|在附加过程中发生了安全冲突。|  
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|桌面程序不能附加到调试器。|  
  
## <a name="remarks"></a>备注  
 调试引擎 (DE) 永远不会调用此方法来附加到的程序。 如果在程序的地址空间中运行 DE [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)调用方法。 如果在 DE 运行中会话调试管理器 (SDM) 地址空间，[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)   
 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
