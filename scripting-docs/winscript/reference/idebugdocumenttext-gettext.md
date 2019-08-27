---
title: IDebugDocumentText::GetText |Microsoft Docs
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
ms.openlocfilehash: 63e1fee3531272f18c85c23ea83b8ca12920bd2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970856"
---
# <a name="idebugdocumenttextgettext"></a>IDebugDocumentText::GetText
检索字符和/或字符位置范围与关联的字符属性。  
  
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
 [in]开始位置范围内的字符位置。  
  
 `pcharText`  
 [in、 out]字符文本缓冲区。 缓冲区必须足够大以保存`cMaxChars`字符。 如果此参数为 NULL，则该方法不返回字符。  
  
 `pstaTextAttr`  
 [in、 out]字符属性缓冲区。 缓冲区必须足够大以保存`cMaxChars`字符。 如果此参数为 NULL，则该方法不返回特性。  
  
 `pcNumChars`  
 [in、 out]返回字符/属性数。 此参数必须设置为零之前调用此方法。  
  
 `cMaxChars`  
 [in]中的字符位置范围的字符数。 此外指定要返回字符最大的数目。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法检索字符和/或字符位置范围与关联的字符属性。 字符位置范围被指定字符位置和字符数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)   
 [SOURCE_TEXT_ATTR 枚举](../../winscript/reference/source-text-attr-enumeration.md)