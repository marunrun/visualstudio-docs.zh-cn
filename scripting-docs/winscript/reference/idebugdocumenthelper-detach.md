---
title: IDebugDocumentHelper：:D etach |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.Detach
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::Detach
ms.assetid: 820b9a8c-9a88-479a-b095-daea99394f9c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 876e23d3466352cb244cc445b2435f556bb88160
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576966"
---
# <a name="idebugdocumenthelperdetach"></a>IDebugDocumentHelper::Detach
从文档树中删除此文档。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Detach();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法从文档树中删除此文档。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper：： Attach](../../winscript/reference/idebugdocumenthelper-attach.md)    
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)