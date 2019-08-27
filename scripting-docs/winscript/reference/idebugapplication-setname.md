---
title: IDebugApplication::SetName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.SetName
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::SetName
ms.assetid: 7b0ddc58-6f20-4ce3-9bdf-81a6c1d64256
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4ac0b253d5193fc507e2d74a2d9dbcdd893e9fdb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990768"
---
# <a name="idebugapplicationsetname"></a>IDebugApplication::SetName
设置应用程序的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetName(  
   LPCOLESTR  pstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrName`  
 [in]应用程序的名称。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 在后续调用返回提供给此方法的名称`IRemoteDebugApplication::GetName`方法。  
  
 应在调用之前调用此方法`IProcessDebugManager::AddApplication`方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)