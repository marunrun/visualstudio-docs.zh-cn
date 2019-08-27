---
title: 'Idebugdocumenthelper:: Attach |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.Attach
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::Attach
ms.assetid: 834f23a9-716d-44df-b23c-d1bf6da60e79
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8f4fbd1686d27e594b748ca97c82c645de1b93de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62783130"
---
# <a name="idebugdocumenthelperattach"></a>IDebugDocumentHelper::Attach
将此文档添加到文档树。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Attach(  
   IDebugDocumentHelper*  pddhParent  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pddhParent`  
 [in]本文档的将其添加在文档树。 可以为 NULL。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将此文档添加到文档树、 使用`pddhParent`作为父级。 如果`pddhParent`是`NULL`，本文档将是顶级文档。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper::Detach](../../winscript/reference/idebugdocumenthelper-detach.md)   
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)