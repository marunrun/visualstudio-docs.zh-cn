---
title: IDebugDocumentTextAuthor::ReplaceText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextAuthor.ReplaceText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextAuthor::ReplaceText
ms.assetid: f89304e6-5be0-45a5-947d-2c59c3c0a05e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 920b6851f5fea42597be7ec5dcc55350024abea9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946760"
---
# <a name="idebugdocumenttextauthorreplacetext"></a>IDebugDocumentTextAuthor::ReplaceText
替换文档中的文本。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ReplaceText(  
   ULONG    cCharacterPosition,  
   ULONG    cNumToReplace,  
   OLECHAR  pcharText[]  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 [in]启动要替换的字符范围的位置。  
  
 `cNumToReplace`  
 [in]要替换的字符数。  
  
 `pcharText[]`  
 [in]包含要替换旧的字符的新字符的缓冲区。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将替换文档中的文本。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentTextAuthor 接口](../../winscript/reference/idebugdocumenttextauthor-interface.md)