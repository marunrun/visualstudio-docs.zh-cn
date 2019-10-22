---
title: IDebugStackFrameSnifferEx：： EnumStackFramesEx |Microsoft Docs
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
ms.openlocfilehash: 6a4062e7c0a9b3a82578daffa2ab7ef7e9ba614d
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576712"
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
 中枚举堆栈帧的地址限制较低。  
  
 `ppedsf`  
 弄当前线程的堆栈帧的枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 堆栈帧枚举器返回从堆栈顶部开始、最近推送的帧的帧。 枚举器仅包含地址大于或等于 `dwSpMin` 的堆栈帧。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrameSnifferEx 接口](../../winscript/reference/idebugstackframesnifferex-interface.md)