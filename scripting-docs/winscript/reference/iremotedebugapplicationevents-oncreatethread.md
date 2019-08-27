---
title: IRemoteDebugApplicationEvents::OnCreateThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationEvents.OnCreateThread
apilocation:
- jscript.dll
helpviewer_keywords:
- IRemoteDebugApplicationEvents::OnCreateThread
ms.assetid: 0b7c5181-eda6-4303-b4ae-d45962e8a3d3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 64317666fe5c449207c2eedac550ca6a1effc1ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943633"
---
# <a name="iremotedebugapplicationeventsoncreatethread"></a>IRemoteDebugApplicationEvents::OnCreateThread
处理在创建线程事件。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnCreateThread(  
   IRemoteDebugApplicationThread*  prdat  
);  
```  
  
#### <a name="parameters"></a>参数  
 `prdat`  
 [in]新创建的线程。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法可处理在创建线程事件。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplicationEvents 接口](../../winscript/reference/iremotedebugapplicationevents-interface.md)