---
title: 'Idebugdocumenthelper:: Getdebugapplicationnode |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.GetDebugApplicationNode
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::GetDebugApplicationNode
ms.assetid: ecd18803-beb4-4ac2-9702-cc9e8a12c395
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 10740c3489b617b1685ad222cac7c158e0196c4d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62783078"
---
# <a name="idebugdocumenthelpergetdebugapplicationnode"></a>IDebugDocumentHelper::GetDebugApplicationNode
返回对应于本文档的调试应用程序节点。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDebugApplicationNode(  
   IDebugApplicationNode**  ppdan  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppdan`  
 [out]对应于本文档的调试应用程序节点。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 返回对应于本文档的调试应用程序节点。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)