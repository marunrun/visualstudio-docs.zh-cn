---
title: IDebugDocumentHost::GetFileName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.GetFileName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::GetFileName
ms.assetid: b814a848-8a3d-468d-9282-c5c0354b22a1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 511cdb40a5bb0f885fed8b811a095e7a53a8bb6f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971103"
---
# <a name="idebugdocumenthostgetfilename"></a>IDebugDocumentHost::GetFileName
返回不包含路径信息的文档的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetFileName(  
   BSTR*  pbstrShortName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrShortName`  
 [out]包含文档的短名称的字符串。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回文档不包含路径信息的短的名称。 短名称通常使用情况如**另存为...** 对话框。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)