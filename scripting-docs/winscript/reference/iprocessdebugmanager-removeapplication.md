---
title: IProcessDebugManager::RemoveApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.RemoveApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::RemoveApplication
ms.assetid: 334e869d-81ae-4d30-9e89-89763ad4f184
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5c357fa5587d4fc5bf8c1752e20e7e0aa9df9835
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944781"
---
# <a name="iprocessdebugmanagerremoveapplication"></a>IProcessDebugManager::RemoveApplication
删除应用程序从正在运行的应用程序列表。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT RemoveApplication(  
   DWORD  dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwAppCookie`  
 [in]提供的 cookie`IProcessDebugManager::AddApplication`应用程序添加到应用程序列表中时。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法删除应用程序从正在运行的应用程序列表。  
  
## <a name="see-also"></a>请参阅  
 [IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)   
 [IProcessDebugManager 接口](../../winscript/reference/iprocessdebugmanager-interface.md)