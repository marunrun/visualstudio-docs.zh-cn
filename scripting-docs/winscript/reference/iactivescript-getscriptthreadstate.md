---
title: IActiveScript::GetScriptThreadState | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptThreadState
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptThreadState
ms.assetid: 7cac94d0-436e-4c29-895b-0c4afa0b3ccc
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a0066894830c111a8e0ad18f7acdc09d6114162e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935598"
---
# <a name="iactivescriptgetscriptthreadstate"></a>IActiveScript::GetScriptThreadState
检索脚本线程的当前的状态。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptThreadState(  
    SCRIPTTHREADID stidThread,    // identifier of script thread  
    SCRIPTTHREADSTATE *pstsState  // receives state flag  
);  
```  
  
#### <a name="parameters"></a>参数  
 `stidThread`  
 [in]为其状态所需的线程的标识符或下列特殊线程标识符之一：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTHREADID_BASE|基础线程;也就是说，在其中的脚本引擎的线程已实例化。|  
|SCRIPTTHREADID_CURRENT|当前正在执行的线程。|  
  
 `pstsState`  
 [out]一个变量来接收指示线程的状态的地址。 状态将由定义的命名常量值之一[SCRIPTTHREADSTATE 枚举](../../winscript/reference/scriptthreadstate-enumeration.md)枚举。 如果此参数不会标识当前线程，随时可能更改状态。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
  
## <a name="remarks"></a>备注  
 此方法可以从非基础线程调用不会导致到主机对象或一个非基本标注[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)