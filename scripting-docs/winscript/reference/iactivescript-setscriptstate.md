---
title: IActiveScript::SetScriptState | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.SetScriptState
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_SetScriptState
ms.assetid: f2b2700c-0c8d-40db-ad84-dc751c5d9bc2
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 16a13b545ddd482f8aa143d289d46447370e23ac
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935526"
---
# <a name="iactivescriptsetscriptstate"></a>IActiveScript::SetScriptState
将脚本引擎放入给定状态。 此方法可以从非基础线程调用不会导致到主机对象或一个非基本标注[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetScriptState(  
    SCRIPTSTATE ss  // identifier of new state  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ss`  
 [in]将脚本引擎设置为给定的状态。 可以是中定义的值之一[SCRIPTSTATE 枚举](../../winscript/reference/scriptstate-enumeration.md)枚举。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_FAIL`|脚本引擎不支持转换为初始化状态。 主机必须放弃此脚本引擎和创建、 初始化和加载新的脚本引擎来达到同样的效果。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化），因此失败。|  
|`OLESCRIPT_S_PENDING`|已成功，该方法已排入队列但尚未未更改状态。 当状态更改，站点将返回通过调用[IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)方法。|  
|`S_FALSE`|该方法成功，但该脚本已处于给定状态。|  
  
## <a name="remarks"></a>备注  
 有关脚本引擎状态的详细信息，请参阅脚本引擎状态章节[Windows 脚本引擎](../../winscript/windows-script-engines.md)。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript::Clone](../../winscript/reference/iactivescript-clone.md)   
 [IActiveScript::GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)   
 [IActiveScriptParse::ParseScriptText](../../winscript/reference/iactivescriptparse-parsescripttext.md)   
 [IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)