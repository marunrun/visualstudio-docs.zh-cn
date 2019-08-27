---
title: IDebugFormatter::GetVariantForString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugFormatter.GetVariantForString
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugFormatter::GetVariantForString
ms.assetid: 2993431d-0ee2-4d8d-b62c-0a810a8bc391
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea6cd1f77481282700de492e2857046044a04e2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979284"
---
# <a name="idebugformattergetvariantforstring"></a>IDebugFormatter::GetVariantForString
返回包含给定的字符串的变量。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetVariantForString(  
   LPCOLESTR  pwstrValue,  
   VARIANT*   pvar  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pwstrValue`  
 [in]若要在一个变量中存储的字符串。  
  
 `pvar`  
 [out]变体包含`pwstrValue`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回包含给定的字符串的变量。  
  
## <a name="see-also"></a>请参阅  
 [IDebugFormatter 接口](../../winscript/reference/idebugformatter-interface.md)