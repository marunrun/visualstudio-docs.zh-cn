---
title: 'Ijsenumdebugproperty:: Next 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsEnumDebugProperty.Next
apilocation:
- jscript9diag.dll
ms.assetid: 9fad1893-483a-440c-88c1-469494212300
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3ec6a1dded8c24de06a5746261a19b6609a97ada
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977534"
---
# <a name="ijsenumdebugpropertynext-method"></a>IJsEnumDebugProperty::Next 方法
读取此对象的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next(  
   ULONG count,  
   IJsDebugProperty **ppDebugProperty,  
   ULONG *pActualCount  
);  
```  
  
#### <a name="parameters"></a>参数  
 `count`  
 [in]要读取的属性数。  
  
 `ppDebugProperty`  
 [out]表示属性浏览器的对象。  
  
 `pActualCount`  
 [out]对象的属性的实际数目。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsEnumDebugProperty 接口](../../winscript/reference/ijsenumdebugproperty-interface.md)