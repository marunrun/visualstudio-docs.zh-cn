---
title: IActiveScriptSite::OnScriptTerminate |Microsoft Docs
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
ms.openlocfilehash: 664f974b26a2cae0d1e16d37dc3bc66e95993d6f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992653"
---
# <a name="iactivescriptsiteonscriptterminate"></a>IActiveScriptSite::OnScriptTerminate
通知主机脚本已完成执行。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnScriptTerminate(  
    VARIANT *pvarResult,   // address of script results  
    EXCEPINFO *pexcepinfo  // address of structure with exception information  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvarResult`  
 [in]包含脚本结果中，将变量的地址或`NULL`如果脚本不生成任何结果。  
  
 `pexcepinfo`  
 [in]地址`EXCEPINFO`结构，其中包含异常信息时该脚本终止，生成或`NULL`如果不生成任何异常。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="remarks"></a>备注  
 脚本引擎将调用此方法之前调用[IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)完成方法，设置了 SCRIPTSTATE_INITIALIZED 标志。 此方法可用于完成状态和结果返回到主机。 请注意，许多脚本语言，基于主机的接收器事件，由主机定义的有效期。 在这种情况下，可能永远不会调用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)