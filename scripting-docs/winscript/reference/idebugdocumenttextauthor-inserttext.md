---
title: IDebugDocumentTextAuthor::InsertText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextAuthor.InsertText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextAuthor::InsertText
ms.assetid: ef4e6a5b-8efa-4290-b498-c0f8a6aac09b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 678e2429e98f268d65f9c29704e2e9d5a1a8538c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970895"
---
# <a name="idebugdocumenttextauthorinserttext"></a>IDebugDocumentTextAuthor::InsertText
将新的文本插入到文档。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT InsertText(  
   ULONG    cCharacterPosition,  
   ULONG    cNumToInsert,  
   OLECHAR  pcharText[]  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 [in]要插入文本的位置。  
  
 `cNumToInsert`  
 [in]要插入的字符数。  
  
 `pcharText[]`  
 [in]包含要插入的字符的缓冲区。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将新的文本插入到文档。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentTextAuthor 接口](../../winscript/reference/idebugdocumenttextauthor-interface.md)   
 [IDebugDocumentTextAuthor::RemoveText](../../winscript/reference/idebugdocumenttextauthor-removetext.md)