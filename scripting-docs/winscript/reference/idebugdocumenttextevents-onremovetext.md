---
title: IDebugDocumentTextEvents::onRemoveText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextEvents.onRemoveText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextEvents::onRemoveText
ms.assetid: c5dfe674-c42f-4e57-9d48-8380d5aa206b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 506d7c5349cf074ce4a4cbe60e33459a09a91b67
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946708"
---
# <a name="idebugdocumenttexteventsonremovetext"></a>IDebugDocumentTextEvents::onRemoveText
指示已从文档中删除文本。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onRemoveText(  
   ULONG  cCharacterPosition,  
   ULONG  cNumToRemove  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 [in]删除第一个字符的字符位置。  
  
 `cNumToRemove`  
 [in]删除的字符数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法指示已从文档中删除文本。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentTextEvents 接口](../../winscript/reference/idebugdocumenttextevents-interface.md)   
 [IDebugDocumentTextEvents::onInsertText](../../winscript/reference/idebugdocumenttextevents-oninserttext.md)