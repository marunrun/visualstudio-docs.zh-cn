---
title: IDebugStackFrameSnifferEx::EnumStackFramesEx | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugStackFrameSnifferEx.EnumStackFramesEx
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugStackFrameSnifferEx::EnumStackFramesEx
ms.assetid: b656b581-aff0-4984-8d8a-a1c7a8e6558a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8969c279e4eb2c2966e297317a25a60f12be68a9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005714"
---
# <a name="idebugstackframesnifferexenumstackframesex"></a>IDebugStackFrameSnifferEx::EnumStackFramesEx
返回当前线程的堆栈帧的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumStackFramesEx(  
   DWORD_PTR                dwSpMin,  
   IEnumDebugStackFrames**  ppedsf  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwSpMin`  
 [in]枚举堆栈帧的较低的地址限制。  
  
 `ppedsf`  
 [out]当前线程的堆栈帧的枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 堆栈帧枚举器返回具有最新入栈帧的堆栈顶部开始的帧。 枚举数包含仅具有地址大于或等于堆栈帧`dwSpMin`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrameSnifferEx 接口](../../winscript/reference/idebugstackframesnifferex-interface.md)