---
title: IDebugHelper::CreatePropertyBrowser |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugHelper.CreatePropertyBrowser
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugHelper::CreatePropertyBrowser
ms.assetid: 2fa819cf-c7f7-4bd7-b018-ea33b804ba8f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4fc1e4365deea4a3981d9cf457a2c0af37edcd43
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979248"
---
# <a name="idebughelpercreatepropertybrowser"></a>IDebugHelper::CreatePropertyBrowser
返回包装一个变体的属性浏览器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreatePropertyBrowser(  
   VARIANT*                  pvar,  
   LPCOLESTR                 bstrName,  
   IDebugApplicationThread*  pdat,  
   IDebugProperty**          ppdob  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvar`  
 [in]若要浏览的根变体。  
  
 `bstrName`  
 [in]提供给根名称。  
  
 `pdat`  
 [in]线程在其请求属性。 如果此参数为 NULL，则执行没有封送处理。  
  
 `ppdob`  
 [out]属性浏览器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回包装一个变体的属性浏览器。  
  
## <a name="see-also"></a>请参阅  
 [IDebugHelper::CreatePropertyBrowserEx](../../winscript/reference/idebughelper-createpropertybrowserex.md)   
 [IDebugHelper 接口](../../winscript/reference/idebughelper-interface.md)   
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)