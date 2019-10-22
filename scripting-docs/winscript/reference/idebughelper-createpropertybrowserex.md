---
title: IDebugHelper：： CreatePropertyBrowserEx |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugHelper.CreatePropertyBrowserEx
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugHelper::CreatePropertyBrowserEx
ms.assetid: 87ad322f-09da-4ce8-bb68-0b0bbeec645b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4d64d9dad54e029dc4c76e8b7e6c7a3f0299b0cb
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576503"
---
# <a name="idebughelpercreatepropertybrowserex"></a>IDebugHelper::CreatePropertyBrowserEx
返回一个属性浏览器，该浏览器包装变体，并允许对变体值或 VARTYPE 类型的自定义转换为字符串。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreatePropertyBrowserEx(  
   VARIANT*                  pvar,  
   LPCOLESTR                 bstrName,  
   IDebugApplicationThread*  pdat,  
   IDebugFormatter*          pdf,  
   IDebugProperty**          ppdob  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvar`  
 中要浏览的根变体。  
  
 `bstrName`  
 中要为根指定的名称。  
  
 `pdat`  
 中要请求其属性的线程。 如果此参数为 NULL，则不执行任何封送处理。  
  
 `pdf`  
 中为变体提供自定义格式设置的对象。  
  
 `ppdob`  
 弄属性浏览器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回包装变体的属性浏览器，并允许将变体值或 VARTYPE 类型的自定义转换为字符串。  
  
## <a name="see-also"></a>请参阅  
 [IDebugHelper：： CreatePropertyBrowser](../../winscript/reference/idebughelper-createpropertybrowser.md)    
 [IDebugHelper 接口](../../winscript/reference/idebughelper-interface.md)   
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)