---
title: IEnumDebugStackFrames：： Next |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugStackFrames.Next
apilocation:
- jscript.dll
helpviewer_keywords:
- IEnumDebugStackFrames::Next
ms.assetid: ade3f5b0-8ff3-48a0-9433-270789e6d53e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 17261f8ba9b2957d33ed7019c16f2e1423b6b42e
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575552"
---
# <a name="ienumdebugstackframesnext"></a>IEnumDebugStackFrames::Next
检索枚举序列中指定数量的段。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next(  
   ULONG                       celt,  
   DebugStackFrameDescriptor*  prgdsfd,  
   ULONG*                      pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 中要检索的段数。  
  
 `prgdsfd`  
 弄返回一个 `DebugStackFrameDescriptor` 接口数组，该数组表示要检索的段。  
  
 `pceltFetched`  
 弄枚举器提取的实际段数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法检索枚举序列中指定数量的段。  
  
## <a name="see-also"></a>另请参阅  
 [IEnumDebugStackFrames 接口](../../winscript/reference/ienumdebugstackframes-interface.md)   
 [DebugStackFrameDescriptor 结构](../../winscript/reference/debugstackframedescriptor-structure.md)