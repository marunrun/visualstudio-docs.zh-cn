---
title: IDebugApplication：： HandleBreakPoint |Microsoft Docs
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
ms.openlocfilehash: 30937817424e88f80cfa6afa8c874adfd2b2687b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574963"
---
# <a name="idebugapplicationhandlebreakpoint"></a>IDebugApplication::HandleBreakPoint
导致当前线程阻止断点通知并将其发送到调试器 IDE。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT HandleBreakPoint(  
   BREAKREASON         br,  
   BREAKRESUMEACTION*  pbra  
);  
```  
  
#### <a name="parameters"></a>参数  
 `br`  
 中中断的原因。  
  
 `pbra`  
 弄调试器恢复应用程序时要执行的操作。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎在命中断点的线程的上下文中调用此方法。 此方法阻止当前线程，并将断点通知发送到调试器 IDE。 调试器恢复应用程序时，`pbra` 参数指定要执行的操作。  
  
> [!NOTE]
> 可通过线程调用语言引擎来执行诸如枚举堆栈帧或在断点期间计算表达式等任务。  
  
 此方法导致调用 `IApplicationDebugger::onHandleBreakPoint`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IApplicationDebugger：： onHandleBreakPoint](../../winscript/reference/iapplicationdebugger-onhandlebreakpoint.md)    
 [BREAKREASON 枚举](../../winscript/reference/breakreason-enumeration.md)   
 [BREAKRESUMEACTION 枚举](../../winscript/reference/breakresumeaction-enumeration.md)