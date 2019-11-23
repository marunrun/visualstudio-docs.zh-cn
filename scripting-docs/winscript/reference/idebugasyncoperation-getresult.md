---
title: IDebugAsyncOperation：： GetResult |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.GetResult
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::GetResult
ms.assetid: 56d43365-6b12-4213-a97c-953c40d7b7f6
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 55c51649a5bc3094dd306166e013a892ce67e236
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573285"
---
# <a name="idebugasyncoperationgetresult"></a>IDebugAsyncOperation::GetResult
提供同步调试操作的返回值和返回对象参数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetResult(  
   HRESULT*    phrResult,  
   IUnknown**  ppunkResult  
);  
```  
  
#### <a name="parameters"></a>参数  
 `phrResult`  
 弄如果操作已完成，`phrResult` 为 `IDebugSyncOperation::Execute`的返回值。  
  
 `ppunkResult`  
 弄如果操作已完成，`ppunkResult` 是操作返回的对象参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_PENDING`|操作未完成。|  
  
## <a name="remarks"></a>备注  
 如果操作已完成，则此方法将从 `IDebugSyncOperation::Execute`返回 `HRESULT` 和对象参数。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)