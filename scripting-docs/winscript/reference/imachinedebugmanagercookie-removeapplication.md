---
title: IMachineDebugManagerCookie：： RemoveApplication |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IMachineDebugManagerCookie.RemoveApplication
apilocation:
- scrobj.dll
helpviewer_keywords:
- IMachineDebugManagerCookie::RemoveApplication
ms.assetid: af8f4a52-ec5e-48fa-87de-234d5e6528d0
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d829262245c8c14b83ce4016f103ecae68895bd9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576779"
---
# <a name="imachinedebugmanagercookieremoveapplication"></a>IMachineDebugManagerCookie::RemoveApplication
从正在运行的应用程序列表中删除应用程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT RemoveApplication(  
   DWORD  dwDebugAppCookie,  
   DWORD  dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwDebugAppCookie`  
 中标识调试应用程序的 cookie。  
  
 `dwAppCookie`  
 中将应用程序添加到应用程序列表时提供的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 只要调用 `IProcessDebugManager::RemoveApplication`，进程调试管理器就会调用此方法。  
  
## <a name="see-also"></a>另请参阅  
 [IMachineDebugManagerCookie::AddApplication](../../winscript/reference/imachinedebugmanagercookie-addapplication.md)   
 [IMachineDebugManagerCookie 接口](../../winscript/reference/imachinedebugmanagercookie-interface.md)   
 [IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)