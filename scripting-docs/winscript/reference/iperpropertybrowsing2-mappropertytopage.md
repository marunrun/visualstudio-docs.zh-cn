---
title: IPerPropertyBrowsing2::MapPropertyToPage |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IPerPropertyBrowsing2.MapPropertyToPage
apilocation:
- scrobj.dll
helpviewer_keywords:
- IPerPropertyBrowsing2::MapPropertyToPage
ms.assetid: e6418a8e-500b-42e1-9b5a-52e6f7567f99
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 77270bbe963f281a43a085cb7d15724b7b2ec14e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944835"
---
# <a name="iperpropertybrowsing2mappropertytopage"></a>IPerPropertyBrowsing2::MapPropertyToPage
返回可用于编辑此属性的属性页的 CLSID。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT MapPropertyToPage(  
   DISPID  dispid,  
   CLSID*  pClsidPropPage  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dispid`  
 [in]调度感兴趣的属性的标识符。  
  
 `pClsidPropPage`  
 [out]指针，指向标识与属性关联的属性页的 CLSID。 如果此方法失败，*`pClsidPropPage`设置为 CLSID_NULL。  
  
## <a name="return-value"></a>返回值  
 返回一个有效`HRESULT`，通常`S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IPerPropertyBrowsing2 接口 1](../../winscript/reference/iperpropertybrowsing2-interface-1.md)