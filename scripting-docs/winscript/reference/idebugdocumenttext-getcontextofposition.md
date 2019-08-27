---
title: IDebugDocumentText::GetContextOfPosition | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentText.GetContextOfPosition
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentText::GetContextOfPosition
ms.assetid: 86560853-d9b1-499a-a1b5-ea06aa1f1f5c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: df63362c422289652d45ed4bbc80f117e17fb73c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008712"
---
# <a name="idebugdocumenttextgetcontextofposition"></a>IDebugDocumentText::GetContextOfPosition
创建与提供的字符位置范围对应的文档上下文对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetContextOfPosition(  
   ULONG                    cCharacterPosition,  
   ULONG                    cNumChars,  
   IDebugDocumentContext**  ppsc  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cCharacterPosition`  
 [in]开始位置范围内的字符位置。  
  
 `cNumChars`  
 [in]范围内的字符数。  
  
 `ppsc`  
 [out]对应于指定的字符位置范围的文档上下文对象。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法创建一个对应于提供的字符位置范围的文档上下文对象。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)