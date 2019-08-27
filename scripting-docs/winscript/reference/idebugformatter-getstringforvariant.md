---
title: IDebugFormatter::GetStringForVariant |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugFormatter.GetStringForVariant
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugFormatter::GetStringForVariant
ms.assetid: 95189d03-1126-433e-8513-659107b3df16
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 901bf9648d4d16faf7386b528cc3fd877070a5b6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996852"
---
# <a name="idebugformattergetstringforvariant"></a>IDebugFormatter::GetStringForVariant
返回一个字符串，表示给定的变体值。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetStringForVariant(  
   VARIANT*  pvar,  
   ULONG     nRadix,  
   BSTR*     pbstrValue  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvar`  
 [in]若要表示为一个字符串的变体。  
  
 `nRadix`  
 [in]要用于数字值的基数。  
  
 `pbstrValue`  
 [out]字符串，表示`pvar`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回一个字符串，表示给定变量的值。  
  
## <a name="see-also"></a>请参阅  
 [IDebugFormatter 接口](../../winscript/reference/idebugformatter-interface.md)