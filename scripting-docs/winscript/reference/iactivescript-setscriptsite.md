---
title: IActiveScript：： SetScriptSite |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.SetScriptSite
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_SetScriptSite
ms.assetid: 47d94c32-09f8-4539-ac56-0236026f627b
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 063dcc7b580334bff9780e9c209b621ef7e25656
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575334"
---
# <a name="iactivescriptsetscriptsite"></a>IActiveScript::SetScriptSite
向脚本引擎通知主机提供的[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口站点。 在使用任何其他[IActiveScript](../../winscript/reference/iactivescript.md)接口方法之前调用此方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetScriptSite(  
    IActiveScriptSite *pScriptSite  // address of host script site  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pScriptSite`  
 中要与脚本引擎的此实例关联的主机提供的脚本站点的地址。 必须将站点唯一分配给此脚本引擎实例;不能与其他脚本引擎共享。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_FAIL`|出现未指定的错误;脚本引擎无法完成站点初始化。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，已设置了站点）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)