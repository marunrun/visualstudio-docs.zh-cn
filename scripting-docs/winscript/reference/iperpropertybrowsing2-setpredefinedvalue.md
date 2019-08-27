---
title: IPerPropertyBrowsing2::SetPredefinedValue |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IPerPropertyBrowsing2.SetPredefinedValue
apilocation:
- scrobj.dll
helpviewer_keywords:
- IPerPropertyBrowsing2::SetPredefinedValue
ms.assetid: 3aff5300-c5a4-4d9b-9d47-a75b64014ac4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4d35e087cc057608666e104681d65fa8009f8167
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944821"
---
# <a name="iperpropertybrowsing2setpredefinedvalue"></a>IPerPropertyBrowsing2::SetPredefinedValue
设置指定的属性的值`dispID`。 由标记标识预定义的值 `dwCookie.`  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetPredefinedValue(  
   DISPID  dispid,  
   DWORD  dwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dispid`  
 [in]为其设置预定义的值的属性的调度标识符。  
  
 `dwCookie`  
 [in]标识要设置的值的标记。  
  
## <a name="return-value"></a>返回值  
 返回一个有效`HRESULT`，通常`S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IPerPropertyBrowsing2 接口 1](../../winscript/reference/iperpropertybrowsing2-interface-1.md)