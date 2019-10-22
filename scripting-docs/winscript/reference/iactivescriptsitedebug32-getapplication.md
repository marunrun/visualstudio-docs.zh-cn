---
title: IActiveScriptSiteDebug32：： GetApplication |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 533d770d-06a4-4693-873e-255c9c6f0df0
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 93c4a8fe6e5c2aac8b07f896810dcd03060b46d0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572194"
---
# <a name="iactivescriptsitedebug32getapplication"></a>IActiveScriptSiteDebug32::GetApplication
返回与此脚本网站关联的调试应用程序对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetApplication(  
   IDebugApplication**  ppda  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppda`  
 弄指向与脚本网站关联的调试应用程序对象的指针。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|宿主不直接支持调试。|  
  
## <a name="remarks"></a>备注  
 @No__t_0 方法为智能主机提供了一种方法，用于定义每个脚本所属的应用程序对象。 脚本引擎应尝试调用此方法来获取其包含的应用程序，如果此操作失败，则调用 `IProcessDebugManager::GetDefaultApplication`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteDebug32 接口](../../winscript/reference/iactivescriptsitedebug32-interface.md)   
 [IProcessDebugManager::GetDefaultApplication](../../winscript/reference/iprocessdebugmanager-getdefaultapplication.md)