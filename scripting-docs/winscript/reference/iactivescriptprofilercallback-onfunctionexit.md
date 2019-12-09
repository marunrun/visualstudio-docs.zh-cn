---
title: IActiveScriptProfilerCallback：： OnFunctionExit |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.OnFunctionExit
apilocation:
- scrobj.dll
ms.assetid: a5d21715-2b0b-423e-8644-f04a9e7cde3d
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 87801b7873e43498031264ff4719fb47eca99f40
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571681"
---
# <a name="iactivescriptprofilercallbackonfunctionexit"></a>IActiveScriptProfilerCallback::OnFunctionExit
通知探查器对象：脚本引擎已执行不是调用文档对象模型（DOM）的函数调用。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnFunctionExit(  
    [in] PROFILER_TOKEN scriptId,   
    [in] PROFILER_TOKEN functionId);  
```  
  
#### <a name="parameters"></a>参数  
 `scriptId`  
 中函数所属脚本的唯一 ID。 此 ID 由脚本引擎分配。  
  
 `functionId`  
 中函数的唯一 ID。 此 ID 由脚本引擎分配。  
  
## <a name="return-value"></a>返回值  
 脚本引擎将忽略此方法的返回值。  
  
## <a name="remarks"></a>备注  
 对于 DOM 调用，脚本引擎将调用[IActiveScriptProfilerCallback2：： OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)而不是 `IActiveScriptProfilerCallback::OnFunctionExit`。 这是因为 DOM 中存在大量的唯一方法和属性。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)   
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)