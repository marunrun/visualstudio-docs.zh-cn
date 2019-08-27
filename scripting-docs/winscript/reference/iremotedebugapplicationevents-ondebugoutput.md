---
title: IRemoteDebugApplicationEvents::OnDebugOutput | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationEvents.OnDebugOutput
apilocation:
- jscript.dll
helpviewer_keywords:
- IRemoteDebugApplicationEvents::OnDebugOutput
ms.assetid: db08872e-3d84-4d7f-bf94-a851bf43a333
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2c7f4c6572a7b06a8ab0ca78419b0bd6518f0e55
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974457"
---
# <a name="iremotedebugapplicationeventsondebugoutput"></a>IRemoteDebugApplicationEvents::OnDebugOutput
处理调试器输出事件。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnDebugOutput(  
   LPCOLESTR  pstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstr`  
 [in]调试输出字符串。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法可处理调试器输出事件。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplicationEvents 接口](../../winscript/reference/iremotedebugapplicationevents-interface.md)