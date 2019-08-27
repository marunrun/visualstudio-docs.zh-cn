---
title: IDebugStackFrameSniffer::EnumStackFrames |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugStackFrameSniffer.EnumStackFrames
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugStackFrameSniffer::EnumStackFrames
ms.assetid: a7629ab3-ef7d-4bbe-a137-bb2a8ad0f384
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: da0d6d46a3bbc508308c689b4e10bea15501fad3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005727"
---
# <a name="idebugstackframesnifferenumstackframes"></a>IDebugStackFrameSniffer::EnumStackFrames
返回当前线程的堆栈帧的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumStackFrames(  
   IEnumDebugStackFrames**  ppedsf  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppedsf`  
 [out]当前线程的堆栈帧的枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 堆栈帧枚举器返回的帧的堆栈顶部开始从最新入栈帧开始。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrameSniffer 接口](../../winscript/reference/idebugstackframesniffer-interface.md)