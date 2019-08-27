---
title: IDebugDocumentInfo::GetDocumentClassId | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentInfo.GetDocumentClassId
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentInfo::GetDocumentClassId
ms.assetid: 3b858794-2c0c-42ba-b98c-cd820ebace20
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c9e86c42954fafd4135956845f9465629cde9990
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971077"
---
# <a name="idebugdocumentinfogetdocumentclassid"></a>IDebugDocumentInfo::GetDocumentClassId
返回`CLSID`标识文档类型。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocumentClassId(  
   CLSID*  pclsidDocument  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pclsidDocument`  
 [out]一个`CLSID`标识文档类型。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法允许主机自定义查看器的调试器 IDE 为此文档。  
  
 如果文档不具有可查看的数据，返回值`pclsidDocument`是`CLSID_NULL`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentInfo 接口](../../winscript/reference/idebugdocumentinfo-interface.md)