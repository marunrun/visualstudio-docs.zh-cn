---
title: IMachineDebugManager::RemoveApplication | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManager.RemoveApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManager::RemoveApplication
ms.assetid: 873509ce-e638-484a-b2a2-489a8ce7dbfe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0ee70097ab87406d6ad39b244bdec61a72aea836
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977547"
---
# <a name="imachinedebugmanagerremoveapplication"></a>IMachineDebugManager::RemoveApplication
删除应用程序从正在运行的应用程序列表。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT RemoveApplication(  
   DWORD  dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwAppCookie`  
 [in]应用程序已添加到应用程序列表时提供的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 进程调试管理器调用此方法时`IProcessDebugManager::RemoveApplication`调用。  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManager::AddApplication](../../winscript/reference/imachinedebugmanager-addapplication.md)   
 [IMachineDebugManager 接口](../../winscript/reference/imachinedebugmanager-interface.md)   
 [IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)