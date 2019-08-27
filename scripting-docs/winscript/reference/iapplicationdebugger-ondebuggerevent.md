---
title: IApplicationDebugger::onDebuggerEvent |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.onDebuggerEvent
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::onDebuggerEvent
ms.assetid: 82a5faaa-1222-4bf1-8569-10439dbdf16d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b78bb3345463dfd682534dc60a216f3e0e8fdf2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991367"
---
# <a name="iapplicationdebuggerondebuggerevent"></a>IApplicationDebugger::onDebuggerEvent
处理自定义应用程序事件。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onDebuggerEvent(  
   REFIID     riid,  
   IUnknown*  punk  
);  
```  
  
#### <a name="parameters"></a>参数  
 `riid`  
 [in]对象的接口标识符。  
  
 `punk`  
 [in]事件对象，用于实现所定义接口`riid`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|目前尚未实现该方法。|  
  
## <a name="remarks"></a>备注  
 语义`IUnknown`是完全定义的应用程序/调试器。  
  
 此方法允许为调试器模型; 的自定义扩展插件目前尚未实现。  
  
 将调用此方法`IDebugApplication::FireDebuggerEvent`调用。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebugger 接口](../../winscript/reference/iapplicationdebugger-interface.md)   
 [IDebugApplication::FireDebuggerEvent](../../winscript/reference/idebugapplication-firedebuggerevent.md)