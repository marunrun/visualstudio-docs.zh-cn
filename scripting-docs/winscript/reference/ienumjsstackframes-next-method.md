---
title: 'Ienumjsstackframes:: Next 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumJsStackFrames.Next
apilocation:
- jscript9diag.dll
ms.assetid: efceb3a1-9239-4f55-9cbb-94670679988b
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 94e3f478654fadec152aba0690a5474ebbfe02f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963294"
---
# <a name="ienumjsstackframesnext-method"></a>IEnumJsStackFrames::Next 方法
获取指定的帧数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next(  
   ULONG cFrameCount,  
   JS_NATIVE_FRAME *pFrames,  
   ULONG *pcFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cFrameCount`  
 [in]要获取的帧数。  
  
 `pFrames`  
 [out]用于存储帧的数组。  
  
 `pcFetched`  
 [out]返回的帧数。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IEnumJsStackFrames 接口](../../winscript/reference/ienumjsstackframes-interface.md)