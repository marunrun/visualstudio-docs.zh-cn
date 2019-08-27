---
title: IActiveScript::GetScriptState | Microsoft Docs
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
ms.openlocfilehash: 0f9f3bedee9af9ae3cb145108d801f252267d5d2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935743"
---
# <a name="iactivescriptgetscriptstate"></a>IActiveScript::GetScriptState
检索脚本引擎的当前的状态。 此方法可以从非基础线程调用不会导致到主机对象或一个非基本标注[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptState(  
    SCRIPTSTATE *pss  // address of structure for state information  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pss`  
 [out]一个变量的地址来接收中定义的值[SCRIPTSTATE 枚举](../../winscript/reference/scriptstate-enumeration.md)枚举。 值指示调用线程与关联的脚本引擎的当前状态。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_POINTER`如果指定了无效的指针。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)