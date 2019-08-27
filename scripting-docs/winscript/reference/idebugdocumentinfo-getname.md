---
title: IDebugDocumentInfo::GetName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentInfo.GetName
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentInfo::GetName
ms.assetid: c25d73da-99b6-4c9f-82af-182b4853f81c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9975563c27b986190fbd2731c3f36b1e32719c0b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970960"
---
# <a name="idebugdocumentinfogetname"></a>IDebugDocumentInfo::GetName
返回指定的文档名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetName(  
   DOCUMENTNAMETYPE  dnt,  
   BSTR*             pbstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dnt`  
 [in]要返回的文档名称的类型。  
  
 `pbstrName`  
 [out]包含名称的字符串。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|指定的文档名称未知。|  
  
## <a name="remarks"></a>备注  
 此方法返回指定的文档名称。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentInfo 接口](../../winscript/reference/idebugdocumentinfo-interface.md)   
 [DOCUMENTNAMETYPE 枚举](../../winscript/reference/documentnametype-enumeration.md)