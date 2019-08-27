---
title: IActiveScript::SetScriptSite | Microsoft Docs
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
ms.openlocfilehash: 3fdf5f3ae84d1a991d67170b5f2b02114b91ee05
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935549"
---
# <a name="iactivescriptsetscriptsite"></a>IActiveScript::SetScriptSite
通知的脚本引擎[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口由主机提供的站点。 任何其他之前调用此方法[IActiveScript](../../winscript/reference/iactivescript.md)使用接口方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetScriptSite(  
    IActiveScriptSite *pScriptSite  // address of host script site  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pScriptSite`  
 [in]要与脚本引擎的此实例相关联的主机提供的脚本站点地址。 站点必须唯一地分配给此脚本的引擎实例;它不能与其他脚本引擎共享。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_FAIL`|出现未知的错误;脚本引擎无法完成正在初始化站点。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，已设置站点）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)