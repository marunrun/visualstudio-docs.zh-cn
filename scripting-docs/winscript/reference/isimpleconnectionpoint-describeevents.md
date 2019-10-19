---
title: ISimpleConnectionPoint：:D escribeEvents |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISimpleConnectionPoint.DescribeEvents
apilocation:
- pdm.dll
helpviewer_keywords:
- ISimpleConnectionPoint::DescribeEvents
ms.assetid: 659ea05f-d41e-424a-bb38-df7672b2d135
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b5000689d588fe3f63ec5408893187bba8d13d63
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571818"
---
# <a name="isimpleconnectionpointdescribeevents"></a>ISimpleConnectionPoint::DescribeEvents
返回指定事件范围内每个事件的 DISPID 和名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT DescribeEvents(  
   ULONG    iEvent,  
   ULONG    cEvents,  
   DISPID*  prgid,  
   BSTR*    prgbstr,  
   ULONG*   pcEventsFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `iEvent`  
 中要检索的第一个事件的索引。  
  
 `cEvents`  
 中要检索的事件数。  
  
 `prgid`  
 弄事件 DISPID 值的数组。  
  
 `prgbstr`  
 弄事件名称的数组。  
  
 `pcEventsFetched`  
 弄提取的实际事件数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`S_FALSE`|请求的事件多于可用的事件数。 不可用事件以 DISPID_NULL 和 NULL BSTR 表示。|  
|`E_INVALIDARG`|无法提取任何元素。|  
  
## <a name="remarks"></a>备注  
 此方法返回指定事件范围内每个事件的 DISPID 和名称。  
  
## <a name="see-also"></a>请参阅  
 [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)