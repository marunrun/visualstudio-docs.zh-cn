---
title: IDebugDocumentText：： GetText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentText.GetText
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentText::GetText
ms.assetid: 3c940a30-6c0f-4deb-aa4d-21a0bdef8461
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6472c40802fff4dad6e5ecc8f2729c95459e09f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572081"
---
# <a name="idebugdocumenttextgettext"></a>IDebugDocumentText::GetText
检索与字符位置范围关联的字符和/或字符特性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetText(  
   ULONG              cCharacterPosition,  
   WCHAR*             pcharText,  
   SOURCE_TEXT_ATTR*  pstaTextAttr,  
   ULONG*             pcNumChars,  
   ULONG              cMaxChars  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 中字符位置范围的起始位置。  
  
 `pcharText`  
 [in，out]字符文本缓冲区。 缓冲区必须足够大才能容纳 `cMaxChars` 字符。 如果此参数为 NULL，则该方法不返回字符。  
  
 `pstaTextAttr`  
 [in，out]字符特性缓冲区。 缓冲区必须足够大才能容纳 `cMaxChars` 字符。 如果此参数为 NULL，则该方法不返回特性。  
  
 `pcNumChars`  
 [in，out]返回的字符/属性的数目。 在调用此方法之前，此参数必须设置为零。  
  
 `cMaxChars`  
 中字符位置范围内的字符数。 还指定要返回的最大字符数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法检索与字符位置范围关联的字符和/或字符特性。 字符位置范围由字符位置和多个字符指定。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)