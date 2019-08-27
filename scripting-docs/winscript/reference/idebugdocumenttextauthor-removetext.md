---
title: IDebugDocumentTextAuthor::RemoveText |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextAuthor.RemoveText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextAuthor::RemoveText
ms.assetid: 2b74d850-c0b1-4a3c-a37c-2c8d06d1ae02
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 989031a6d4b207c69d1a58b2ff99e5797a629440
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007755"
---
# <a name="idebugdocumenttextauthorremovetext"></a>IDebugDocumentTextAuthor::RemoveText
从文档中删除文本。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT RemoveText(  
   ULONG  cCharacterPosition,  
   ULONG  cNumToRemove  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 [in]启动要删除的字符范围的位置。  
  
 `cNumToRemove`  
 [in]要删除的字符数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法从文档中移除文本。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentTextAuthor 接口](../../winscript/reference/idebugdocumenttextauthor-interface.md)   
 [IDebugDocumentTextAuthor::InsertText](../../winscript/reference/idebugdocumenttextauthor-inserttext.md)