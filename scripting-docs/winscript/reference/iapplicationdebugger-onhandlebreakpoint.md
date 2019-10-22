---
title: IApplicationDebugger：： onHandleBreakPoint |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.onHandleBreakPoint
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::onHandleBreakPoint
ms.assetid: 31adcecd-d6c1-4222-ab2c-32ec2fefb322
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3796ea1f50f0c4bcf945dbc10592c048db22757b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577831"
---
# <a name="iapplicationdebuggeronhandlebreakpoint"></a>IApplicationDebugger::onHandleBreakPoint
处理断点事件。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onHandleBreakPoint(  
   IRemoteDebugApplicationThread*  prpt,  
   BREAKREASON                     br,  
   IActiveScriptErrorDebug*        pError  
);  
```  
  
#### <a name="parameters"></a>参数  
 `prpt`  
 中发生断点的线程。  
  
 `br`  
 中断点的原因。  
  
 `pError`  
 中运行时错误信息，在 `br` 的值为 BREAKREASON_ERROR 时提供。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 命中断点并调用 `IDebugApplication::HandleBreakPoint` 时，将调用此方法。  
  
 应用程序将保持挂起状态，直到调试器 IDE 调用 `IRemoteDebugApplication::ResumeFromBreakPoint`。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebugger 接口](../../winscript/reference/iapplicationdebugger-interface.md)   
 [IDebugApplication：： HandleBreakPoint](../../winscript/reference/idebugapplication-handlebreakpoint.md)    
 [IRemoteDebugApplication：： ResumeFromBreakPoint](../../winscript/reference/iremotedebugapplication-resumefrombreakpoint.md)    
 [BREAKREASON 枚举](../../winscript/reference/breakreason-enumeration.md)