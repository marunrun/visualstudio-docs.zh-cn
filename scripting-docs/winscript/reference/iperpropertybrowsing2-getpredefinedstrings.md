---
title: IPerPropertyBrowsing2::GetPredefinedStrings |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IPerPropertyBrowsing2.GetPredefinedStrings
apilocation:
- scrobj.dll
helpviewer_keywords:
- IPerPropertyBrowsing2::GetPredefinedStrings
ms.assetid: d2fa30f7-a566-4dbd-8b47-ffdc00419771
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5a5f71ba91c65a8d99d831c777fc47fe9233fc18
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944858"
---
# <a name="iperpropertybrowsing2getpredefinedstrings"></a>IPerPropertyBrowsing2::GetPredefinedStrings
允许调用方使用的字符串指针，它表示此属性的可能值的计数数组填充列表框。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetPredefinedStrings(  
   DISPID  dispid,  
   CALPOLESTR*  pCaStrings,  
   CADWORD*  pCaCookies  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dispid`  
 [in]调用方为其请求的字符串列表的属性的调度标识符。  
  
 `pCaStrings`  
 [out]指向调用方分配，计数数组结构，其中包含的元素计数和地址的字符串指针的方法分配的数组。 如果方法失败，会分配任何内存，并该结构的内容是不确定。  
  
 `pCaCookies`  
 [out]指向调用方分配的计数数组结构，其中包含的元素数和地址的方法分配的 dword 值数组的指针。 如果方法失败，会分配任何内存，并该结构的内容是不确定。  
  
## <a name="return-value"></a>返回值  
 返回一个有效`HRESULT`，通常`S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IPerPropertyBrowsing2 接口 1](../../winscript/reference/iperpropertybrowsing2-interface-1.md)