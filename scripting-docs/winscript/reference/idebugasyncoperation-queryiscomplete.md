---
title: IDebugAsyncOperation::QueryIsComplete | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.QueryIsComplete
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::QueryIsComplete
ms.assetid: fcf6e229-4d40-46d9-ab81-d3561bc8e084
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: de686f146fded1e4b53914a1de706025f6680ab6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822001"
---
# <a name="idebugasyncoperationqueryiscomplete"></a>IDebugAsyncOperation::QueryIsComplete
确定是否已完成调试操作。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT QueryIsComplete();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|操作已完成。|  
|`S_FALSE`|该操作不完整。|  
  
## <a name="remarks"></a>备注  
 此方法确定是否已完成调试操作。  
  
## <a name="see-also"></a>请参阅  
 [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)