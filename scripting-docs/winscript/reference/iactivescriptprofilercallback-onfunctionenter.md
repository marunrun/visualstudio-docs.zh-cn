---
title: IActiveScriptProfilerCallback::OnFunctionEnter | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.OnFunctionEnter
apilocation:
- scrobj.dll
ms.assetid: 12dab2b4-df4e-444d-99cb-25e1c278e6e8
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1b8410fba08c1799d88532266c022d811c9553fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993379"
---
# <a name="iactivescriptprofilercallbackonfunctionenter"></a>IActiveScriptProfilerCallback::OnFunctionEnter
通知脚本引擎来执行不是到文档对象模型 (DOM) 的调用的函数调用的探查器对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnFunctionEnter(  
    [in] PROFILER_TOKEN scriptId,   
    [in] PROFILER_TOKEN functionId);  
```  
  
#### <a name="parameters"></a>参数  
 `scriptId`  
 [in]该脚本，该函数属于的唯一 ID。 由脚本引擎分配此 ID。  
  
 `functionId`  
 [in]函数的唯一 ID。 由脚本引擎分配此 ID。  
  
## <a name="return-value"></a>返回值  
 此方法的返回值是脚本引擎忽略。  
  
## <a name="remarks"></a>备注  
 对于 DOM 调用，脚本引擎将调用[IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)而不是`IActiveScriptProfilerCallback::OnFunctionEnter`。 这是由于大量的唯一方法和属性的数组。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback::OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)   
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)