---
title: IActiveScriptSiteDebug32::GetApplication | Microsoft Docs
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
ms.openlocfilehash: c71e33445db7745f71e374c586d079a9665776b2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992485"
---
# <a name="iactivescriptsitedebug32getapplication"></a>IActiveScriptSiteDebug32::GetApplication
返回与此脚本站点关联的调试应用程序对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetApplication(  
   IDebugApplication**  ppda  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppda`  
 [out]与脚本站点关联的调试应用程序对象的指针。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|主机不直接支持调试。|  
  
## <a name="remarks"></a>备注  
 `GetApplication`方法提供了智能主机来定义每个脚本所属的应用程序对象的方式。 脚本引擎应尝试调用此方法以获取其包含的应用程序并求助于`IProcessDebugManager::GetDefaultApplication`如果此操作失败。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteDebug32 接口](../../winscript/reference/iactivescriptsitedebug32-interface.md)   
 [IProcessDebugManager::GetDefaultApplication](../../winscript/reference/iprocessdebugmanager-getdefaultapplication.md)