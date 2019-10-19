---
title: IActiveScriptSite：： OnScriptTerminate |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnScriptTerminate
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnScriptTerminate
ms.assetid: 3301ddf4-5929-404c-81d3-1a720e589008
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a715b39b07df4183d4ec542a1dd82b4229d1f41e
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570200"
---
# <a name="iactivescriptsiteonscriptterminate"></a>IActiveScriptSite::OnScriptTerminate
通知宿主脚本已完成执行。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnScriptTerminate(  
    VARIANT *pvarResult,   // address of script results  
    EXCEPINFO *pexcepinfo  // address of structure with exception information  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvarResult`  
 中包含脚本结果的变量的地址，如果脚本未生成任何结果，则为 `NULL`。  
  
 `pexcepinfo`  
 中@No__t_0 结构的地址，该结构包含在脚本终止时生成的异常信息，或者，如果未生成异常，则为 `NULL`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="remarks"></a>备注  
 脚本引擎将在调用[IActiveScriptSite：： OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)方法之前调用此方法，并设置 SCRIPTSTATE_INITIALIZED 标志。 此方法可用于向主机返回完成状态和结果。 请注意，许多基于从主机接收事件的脚本语言都具有主机定义的生命周期。 在这种情况下，可能永远不会调用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)