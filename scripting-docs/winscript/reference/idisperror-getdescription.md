---
title: IDispError::GetDescription | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispError.GetDescription
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDispError::GetDescription
ms.assetid: 04deaea6-0265-4e34-952e-634edba0e923
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5505113ee650c6618be5a95bc77244daf90cfcb7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446946"
---
# <a name="idisperrorgetdescription"></a>IDispError::GetDescription
返回此错误的文本说明。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDescription(  
   BSTR*  pbstrDescription  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrDescription`  
 [out]包含错误的简短说明的字符串。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 在指定的区域设置标识符 (LCID) 传递到的语言中返回的文本`IDispatchEx::InvokeEx`遇到了错误的方法。  
  
> [!NOTE]
> 未实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDispError 接口](../../winscript/reference/idisperror-interface.md)   
 [IDispatchEx::InvokeEx](../../winscript/reference/idispatchex-invokeex.md)