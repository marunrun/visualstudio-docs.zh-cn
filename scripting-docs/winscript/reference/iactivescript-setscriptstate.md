---
title: IActiveScript：： SetScriptState |Microsoft Docs
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
ms.openlocfilehash: ea947e00ffd5a3498261f4a3a8acd4791e8ace60
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577990"
---
# <a name="iactivescriptsetscriptstate"></a>IActiveScript::SetScriptState
使脚本引擎进入给定状态。 此方法可从非基线程调用，而不会导致非基本标注宿主对象或[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetScriptState(  
    SCRIPTSTATE ss  // identifier of new state  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ss`  
 中将脚本引擎设置为给定状态。 可以是在[SCRIPTSTATE 枚举](../../winscript/reference/scriptstate-enumeration.md)枚举中定义的值之一。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_FAIL`|脚本引擎不支持转换回已初始化状态。 宿主必须丢弃此脚本引擎，并创建、初始化和加载新的脚本引擎，以实现同样的效果。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎尚未加载或初始化），因此失败。|  
|`OLESCRIPT_S_PENDING`|此方法已成功排队，但尚未更改状态。 当状态更改时，会通过[IActiveScriptSite：： OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)方法回调站点。|  
|`S_FALSE`|此方法已成功，但该脚本已经处于给定状态。|  
  
## <a name="remarks"></a>备注  
 有关脚本引擎状态的详细信息，请参阅[Windows 脚本引擎](../../winscript/windows-script-engines.md)的脚本引擎状态部分。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript：： Clone](../../winscript/reference/iactivescript-clone.md)    
 [IActiveScript：： GetScriptDispatch](../../winscript/reference/iactivescript-getscriptdispatch.md)    
 [IActiveScript：： InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)    
 [IActiveScriptParse：:P arsescripttext](../../winscript/reference/iactivescriptparse-parsescripttext.md)    
 [IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)