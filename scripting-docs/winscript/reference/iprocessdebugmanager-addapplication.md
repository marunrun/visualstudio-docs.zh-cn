---
title: IProcessDebugManager::AddApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.AddApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::AddApplication
ms.assetid: 73828299-11eb-4c58-ad70-f80f2d0eede8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 206baa92ae8d2803b2b07f4966565755a1785d61
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944970"
---
# <a name="iprocessdebugmanageraddapplication"></a>IProcessDebugManager::AddApplication
将添加到计算机调试管理器的列表正在运行的应用程序的应用程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddApplication(  
   IDebugApplication*  pda,  
   DWORD*              pdwAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pda`  
 [in]调试应用程序将添加到正在运行的应用程序的列表。  
  
 `pdwAppCookie`  
 [out]一个用于从计算机调试管理器删除应用程序的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将添加到正在运行的应用程序在计算机调试管理器中的应用程序列表。  
  
## <a name="see-also"></a>请参阅  
 [IProcessDebugManager 接口](../../winscript/reference/iprocessdebugmanager-interface.md)   
 [IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)