---
title: IDebugProcess2::Attach |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4d4664f164675c445510d8976f33577684dbd1d2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188102"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将会话调试管理器 (SDM) 附加到进程。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Attach(   
   IDebugEventCallback2* pCallback,  
   GUID*                 rgguidSpecificEngines,  
   DWORD                 celtSpecificEngines,  
   HRESULT*              rghrEngineAttach  
);  
```  
  
```csharp  
int Attach(   
   IDebugEventCallback2 pCallback,  
   Guid[]               rgguidSpecificEngines,  
   uint                 celtSpecificEngines,  
   int[]                rghrEngineAttach  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pCallback`  
 [in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)用于调试事件通知的对象。  
  
 `rgguidSpecificEngines`  
 [in]Guid 的数组的调试引擎以用于调试的进程中运行的程序。 此参数可以为 null 值。 有关详细信息，请参阅备注。  
  
 `celtSpecificEngines`  
 [in]引擎中，调试数`rgguidSpecificEngines`数组和大小`rghrEngineAttach`数组。  
  
 `rghrEngineAttach`  
 [in、 out]HRESULT 代码的调试引擎返回的数组。 此数组的大小指定为`celtSpecificEngines`参数。 每个代码通常是`S_OK`或`S_ATTACH_DEFERRED`。 后者表示 DE 当前附加到任何程序。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了其他可能的值。  
  
|值|描述|  
|-----------|-----------------|  
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的进程已附加到调试器。|  
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|在附加过程中发生了安全冲突。|  
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|桌面的过程不能附加到调试器。|  
  
## <a name="remarks"></a>备注  
 附加到进程将 SDM 附加到可调试的调试引擎 (DE) 中指定该进程中运行的所有程序`rgguidSpecificEngines`数组。 设置`rgguidSpecificEngines`参数为 null 值或包含`GUID_NULL`数组中要将附加到进程中的所有程序。  
  
 在过程中发生的所有调试事件都发送到给定[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。 这`IDebugEventCallback2`SDM 调用此方法时提供对象。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
