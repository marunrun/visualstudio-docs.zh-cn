---
title: IActiveScript::GetScriptSite | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptSite
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptSite
ms.assetid: 83a2a89d-93d0-4cbd-9244-91a730cb406b
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b57c4282b7ec77eb4af2ffa983479ae77388e1c9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935766"
---
# <a name="iactivescriptgetscriptsite"></a>IActiveScript::GetScriptSite
检索与 Windows 脚本引擎关联的站点对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptSite(  
    REFIID iid,           // interface identifier  
    void **ppvSiteObject  // address of host site interface  
);  
```  
  
#### <a name="parameters"></a>参数  
 `iid`  
 [in]所请求的接口的标识符。  
  
 `ppvSiteObject`  
 [out]接收主机的站点对象的接口指针的位置的地址。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_NOINTERFACE`|不支持指定的接口。|  
|`E_POINTER`|指定了无效的指针。|  
|`S_FALSE`|没有站点已设置;`ppvSiteObject`参数设置为`NULL`。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)