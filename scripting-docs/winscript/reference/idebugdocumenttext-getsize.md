---
title: IDebugDocumentText::GetSize | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentText.GetSize
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentText::GetSize
ms.assetid: 9da53856-613a-44b2-a84c-99454a2a1548
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 95f8df44a503fa72f57a9cee17eb5e832e4eb670
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008587"
---
# <a name="idebugdocumenttextgetsize"></a>IDebugDocumentText::GetSize
返回文档中的行数和字符数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSize(  
   ULONG*  pcNumLines,  
   ULONG*  pcNumChars  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pcNumLines`  
 [out]在文档中的行数。 如果此参数为 NULL，则该方法不返回值。  
  
 `pcNumChars`  
 [out]在文档中的字符数。 如果此参数为 NULL，则该方法不返回值。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回文档中的行数和字符数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)