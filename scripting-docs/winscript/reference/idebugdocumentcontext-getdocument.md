---
title: IDebugDocumentContext::GetDocument |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentContext.GetDocument
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentContext::GetDocument
ms.assetid: 32db2fea-4938-4644-b39a-8fae05960d1d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9bfcc5b3e2d2e197619f9bc4ec19b55c9eaf1d2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974431"
---
# <a name="idebugdocumentcontextgetdocument"></a>IDebugDocumentContext::GetDocument
返回包含此上下文中的文档。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocument(  
   IDebugDocument**  ppsd  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppsd`  
 [out]包含此上下文中的文档。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 `GetDocument`方法返回包含此上下文中的文档。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentContext 接口](../../winscript/reference/idebugdocumentcontext-interface.md)