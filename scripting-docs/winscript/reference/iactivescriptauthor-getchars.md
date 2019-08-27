---
title: IActiveScriptAuthor::GetChars | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetChars
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetChars
ms.assetid: a73ba263-12f7-4d5f-b4c8-9ad7e2d5d3cb
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 69cdeb16fa0791b3ff8c0cce4a4e67fe110eefc2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935368"
---
# <a name="iactivescriptauthorgetchars"></a>IActiveScriptAuthor::GetChars
返回请求的完成上下文完成字符组。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetChars(  
   DWORD            fRequestedList,  
   BSTR             *pbstrChars  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fRequestedList`  
 [in]请求的完成上下文中。  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_ENUM_TRIGGER|0x0001|请求的左侧和右侧枚举。|  
|SCRIPT_CMPL_MEMBER_TRIGGER|0x0002|请求的成员完成上下文。|  
|SCRIPT_CMPL_PARAM_TRIGGER|0x0003|请求的参数列表。|  
|SCRIPT_CMPL_COMMIT|0x0004|参数列表的请求完成。|  
  
 `pbstrChars`  
 [out]请求的完成上下文所对应的字符。  
  
|`fRequestedList` 参数|返回字符|  
|--------------------------------|-------------------------|  
|SCRIPT_CMPL_ENUM_TRIGGER|"."|  
|SCRIPT_CMPL_MEMBER_TRIGGER|"="|  
|SCRIPT_CMPL_PARAM_TRIGGER|"(,"|  
|SCRIPT_CMPL_COMMIT|"()"|  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)