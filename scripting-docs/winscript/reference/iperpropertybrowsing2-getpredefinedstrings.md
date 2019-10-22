---
title: IPerPropertyBrowsing2：： GetPredefinedStrings |Microsoft Docs
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
ms.openlocfilehash: 55ade724dd9ee5d59feb9d04c5b525ca839a9cec
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576773"
---
# <a name="iperpropertybrowsing2getpredefinedstrings"></a>IPerPropertyBrowsing2::GetPredefinedStrings
允许调用方使用表示此属性的可能值的字符串指针的计数数组填充列表框。  
  
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
 中调用方为其请求字符串列表的属性的调度标识符。  
  
 `pCaStrings`  
 弄指向分配的、计数数组结构的指针，该数组包含方法分配的字符串指针数组的元素计数和地址。 如果该方法失败，则不会分配任何内存，并且不会定义结构的内容。  
  
 `pCaCookies`  
 弄指向分配的、计数数组结构的指针，该数组包含方法分配的 Dword 数组的元素计数和地址。 如果该方法失败，则不会分配任何内存，并且不会定义结构的内容。  
  
## <a name="return-value"></a>返回值  
 返回一个有效 `HRESULT`，通常 `S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IPerPropertyBrowsing2 接口 1](../../winscript/reference/iperpropertybrowsing2-interface-1.md)