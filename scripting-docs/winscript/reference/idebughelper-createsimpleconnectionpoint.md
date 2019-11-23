---
title: IDebugHelper：： CreateSimpleConnectionPoint |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugHelper.CreateSimpleConnectionPoint
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugHelper::CreateSimpleConnectionPoint
ms.assetid: 5e4798ce-6f9f-4184-9853-67bf8c8524ab
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 06324b0d10eb6d0d69b6426276d5df7f382d2abe
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72562453"
---
# <a name="idebughelpercreatesimpleconnectionpoint"></a>IDebugHelper::CreateSimpleConnectionPoint
返回包装给定 `IDispatch` 对象的事件接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateSimpleConnectionPoint(  
   IDispatch*                pdisp  
   ISimpleConnectionPoint**  ppscp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdisp`  
 中要包装的 `IDispatch` 对象。  
  
 `ppscp`  
 弄包装 `pdisp`的事件接口。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 返回包装给定 `IDispatch` 的事件接口（请参阅[ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)）。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugHelper 接口](../../winscript/reference/idebughelper-interface.md)   
 [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)