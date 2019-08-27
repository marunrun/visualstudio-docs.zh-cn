---
title: ISimpleConnectionPoint::DescribeEvents |Microsoft Docs
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
ms.openlocfilehash: 1b5824f945ad25f177fc169b58157377bf53bcce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786414"
---
# <a name="isimpleconnectionpointdescribeevents"></a>ISimpleConnectionPoint::DescribeEvents
在指定范围的事件返回的 DISPID 和每个事件的名称。  
  
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
 [in]要检索的第一个事件的索引。  
  
 `cEvents`  
 [in]要检索的事件数。  
  
 `prgid`  
 [out]事件的 DISPID 值的数组。  
  
 `prgbstr`  
 [out]事件名称的数组。  
  
 `pcEventsFetched`  
 [out]实际提取的事件数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`S_FALSE`|比请求的更多的事件。 使用 DISPID_NULL 和 null BSTR 表示不可用的事件。|  
|`E_INVALIDARG`|无法不提取任何元素。|  
  
## <a name="remarks"></a>备注  
 此方法返回在指定范围的事件的 DISPID 和每个事件的名称。  
  
## <a name="see-also"></a>请参阅  
 [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)