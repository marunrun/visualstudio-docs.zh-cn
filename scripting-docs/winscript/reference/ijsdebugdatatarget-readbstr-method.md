---
title: IJsDebugDataTarget：： ReadBSTR 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.ReadBSTR
apilocation:
- jscript9diag.dll
ms.assetid: 4b571db7-04b9-42a0-9a3e-310ac9d0e659
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b125f58b4be279eac167b803ed6a683c1fb04ddf
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572438"
---
# <a name="ijsdebugdatatargetreadbstr-method"></a>IJsDebugDataTarget::ReadBSTR 方法
从调试目标读取 BSTR。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ReadBSTR(  
   UINT64 address,  
   BSTR *pString  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 中要从中读取的地址。  
  
 `pString`  
 弄从调试目标读取的 BSTR。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 如果地址无效，则返回 E_JsDEBUG_INVALID_MEMORY_ADDRESS。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)