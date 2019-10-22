---
title: IActiveScript：： GetScriptState |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptState
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptState
ms.assetid: 59837f7c-755d-45c4-8194-bd57638fe2e1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d266e713879aafe1c5ca271d46b3030f3275460f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575727"
---
# <a name="iactivescriptgetscriptstate"></a>IActiveScript::GetScriptState
检索脚本引擎的当前状态。 此方法可从非基线程调用，而不会导致非基本标注宿主对象或[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptState(  
    SCRIPTSTATE *pss  // address of structure for state information  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pss`  
 弄用于接收在[SCRIPTSTATE 枚举](../../winscript/reference/scriptstate-enumeration.md)枚举中定义的值的变量的地址。 值指示与调用线程关联的脚本引擎的当前状态。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果指定了无效指针，则返回 `E_POINTER`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)