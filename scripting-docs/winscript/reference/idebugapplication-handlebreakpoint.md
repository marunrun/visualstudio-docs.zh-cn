---
title: IDebugApplication::HandleBreakPoint | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.HandleBreakPoint
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::HandleBreakPoint
ms.assetid: 97219bdf-a39a-4e69-81ac-4ca2afe77ce5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5e3444e6eedde9576216552e41abb0e97aafa2d7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63412382"
---
# <a name="idebugapplicationhandlebreakpoint"></a>IDebugApplication::HandleBreakPoint
导致当前线程被阻塞，并将断点的通知发送到调试器 IDE。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT HandleBreakPoint(  
   BREAKREASON         br,  
   BREAKRESUMEACTION*  pbra  
);  
```  
  
#### <a name="parameters"></a>参数  
 `br`  
 [in]为中断的原因。  
  
 `pbra`  
 [out]在调试器恢复应用程序时要执行的操作。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎遇到断点的线程的上下文中调用此方法。 此方法阻止当前线程，并将断点通知发送到调试器 IDE。 当调试器继续应用程序，`pbra`参数指定要执行的操作。  
  
> [!NOTE]
> 语言引擎不调用由线程执行任务，例如枚举堆栈帧中，或者在该断点的表达式进行计算。  
  
 此方法将导致`IApplicationDebugger::onHandleBreakPoint`调用。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IApplicationDebugger::onHandleBreakPoint](../../winscript/reference/iapplicationdebugger-onhandlebreakpoint.md)   
 [BREAKREASON 枚举](../../winscript/reference/breakreason-enumeration.md)   
 [BREAKRESUMEACTION 枚举](../../winscript/reference/breakresumeaction-enumeration.md)