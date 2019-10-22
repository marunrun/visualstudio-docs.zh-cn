---
title: IDebugAsyncOperation：： Abort |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.Abort
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::Abort
ms.assetid: 232541c6-81b8-4eb7-96a7-a8e5fe087b31
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b9ca6c5e1498229c84dc28a13cda2cce77b58a4f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573295"
---
# <a name="idebugasyncoperationabort"></a>IDebugAsyncOperation::Abort
取消操作。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Abort();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|S_OK|方法成功。|  
|E_NOTIMPL|无法取消操作。|  
  
## <a name="remarks"></a>备注  
 此方法通常从调试器线程中调用，以取消无响应的操作。 此方法导致调用 `IDebugSyncOperation` 对象的 `InProgressAbort` 方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugAsyncOperation：： Start](../../winscript/reference/idebugasyncoperation-start.md)    
 [IDebugSyncOperation::InProgressAbort](../../winscript/reference/idebugsyncoperation-inprogressabort.md)