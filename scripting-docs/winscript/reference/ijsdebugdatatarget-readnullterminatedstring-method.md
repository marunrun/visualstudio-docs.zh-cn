---
title: IJsDebugDataTarget：： ReadNullTerminatedString 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.ReadNullTerminatedString
apilocation:
- jscript9diag.dll
ms.assetid: 64683b39-6fc2-40c4-82ae-2a6f58d392d5
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 67d6ee6c8dad81865767b0b944ef311fc0de0063
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572400"
---
# <a name="ijsdebugdatatargetreadnullterminatedstring-method"></a>IJsDebugDataTarget::ReadNullTerminatedString 方法
从目标读取指定数目的字符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ReadNullTerminatedString(  
   UINT64 address,  
   UINT16 characterSize,  
   UINT32 maxCharacters,  
   BSTR *pString  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 中要从中读取的地址。  
  
 `characterSize`  
 [in] 字符串中每个字符的大小  
  
 `maxCharacters`  
 中要读取的最大字符数。 maxCharacters 应该是合理的。 超过128MB 内存的任何请求都将失败。  如果字符串大于 maxCharacters，则在 maxCharacters 后，结果字符串将被截断。  
  
 `pString`  
 弄从目标读取的 BSTR。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 如果截断，则返回 S_FALSE。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)