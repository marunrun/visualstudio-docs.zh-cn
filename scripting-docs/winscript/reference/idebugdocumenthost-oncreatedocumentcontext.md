---
title: 'Idebugdocumenthost:: Oncreatedocumentcontext |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.OnCreateDocumentContext
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::OnCreateDocumentContext
ms.assetid: 080c8604-cfd7-484e-a337-15040870e683
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a3b614cdc6aad17ab3a4f6e83927b59390005ac2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971090"
---
# <a name="idebugdocumenthostoncreatedocumentcontext"></a>IDebugDocumentHost::OnCreateDocumentContext
通知宿主，新的文档上下文创建，并使宿主可以选择性地返回控制新上下文未知。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnCreateDocumentContext(  
   IUnknown**  ppunkOuter  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppunkOuter`  
 [out]一个对象，用于控制新的上下文。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|主机未提供控制的对象。|  
  
## <a name="remarks"></a>备注  
 此方法允许主机以将新功能添加到提供帮助器文档上下文。 此方法可能会返回**E_NOTIMPL**或 null 的外部对象，在这种情况下调用方负责创建上下文。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)