---
title: IRemoteDebugApplicationThread::SetNextStatement |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationThread.SetNextStatement
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplicationThread::SetNextStatement
ms.assetid: 356766da-f7b7-4e8d-b4f3-2ab8da0609b8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0c4b19322a15e92adcf2609c479af6b21e2078bd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788135"
---
# <a name="iremotedebugapplicationthreadsetnextstatement"></a>IRemoteDebugApplicationThread::SetNextStatement
继续为给定的代码上下文，尽可能地接近给定帧的上下文中的强制执行。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetNextStatement(  
   IDebugStackFrame*   pStackFrame,  
   IDebugCodeContext*  pCodeContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pStackFrame`  
 [in]堆栈帧对象。 此参数可以为 NULL，这意味着应使用当前堆栈帧。  
  
 `pCodeContext`  
 [in]代码上下文。 此参数可以为 NULL，这意味着应使用当前代码上下文。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法强制执行继续到指定的代码上下文尽可能地接近`pCodeContext`，指定的帧的上下文中`pStackFrame`。 这些参数可能是`NULL`，表示当前帧或上下文。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplicationThread 接口](../../winscript/reference/iremotedebugapplicationthread-interface.md)