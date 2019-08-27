---
title: IDebugApplication::FireDebuggerEvent |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.FireDebuggerEvent
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::FireDebuggerEvent
ms.assetid: fd1f602e-fc15-4158-a6e7-497ff5b4a509
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad865f05cc70f462d65d6fbead4143b82a9fa489
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990920"
---
# <a name="idebugapplicationfiredebuggerevent"></a>IDebugApplication::FireDebuggerEvent
触发将泛型事件发送到调试器的`IApplicationDebugger`接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT FireDebuggerEvent(  
   REFGUID    riid,  
   IUnknown*  punk  
);  
```  
  
#### <a name="parameters"></a>参数  
 `riid`  
 [in]对象 GUID。  
  
 `punk`  
 [in]传递到调试器的事件对象。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|目前尚未实现该方法。|  
  
## <a name="remarks"></a>备注  
 GUID 的语义和`IUnknown`是完全定义的应用程序/调试器。  
  
 此方法允许为调试器模型; 的自定义扩展插件目前尚未实现。  
  
 此方法将导致`IApplicationDebugger::onDebuggerEvent`调用。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IApplicationDebugger::onDebuggerEvent](../../winscript/reference/iapplicationdebugger-ondebuggerevent.md)