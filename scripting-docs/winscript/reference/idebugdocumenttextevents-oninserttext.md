---
title: IDebugDocumentTextEvents::onInsertText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentTextEvents.onInsertText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentTextEvents::onInsertText
ms.assetid: 775881de-497a-47a9-86ab-823d77745a72
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4f7f40178d64aaf654850ea54fafee65bc0a1c51
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946721"
---
# <a name="idebugdocumenttexteventsoninserttext"></a>IDebugDocumentTextEvents::onInsertText
指示新的文本已添加到文档。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onInsertText(  
   ULONG  cCharacterPosition,  
   ULONG  cNumToInsert  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 [in]已插入新文本中的字符位置。  
  
 `cNumToInsert`  
 [in]已插入的字符数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 调用此方法是通常由主机渐进式加载内容，如 Web 浏览器。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentTextEvents 接口](../../winscript/reference/idebugdocumenttextevents-interface.md)   
 [IDebugDocumentTextEvents::onRemoveText](../../winscript/reference/idebugdocumenttextevents-onremovetext.md)