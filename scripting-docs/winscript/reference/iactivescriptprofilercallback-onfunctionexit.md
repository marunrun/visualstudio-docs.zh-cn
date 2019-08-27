---
title: IActiveScriptProfilerCallback::OnFunctionExit |Microsoft Docs
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
ms.openlocfilehash: 9c84b64a12b1a6b61399f70b7209c86dd8d2a9a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993327"
---
# <a name="iactivescriptprofilercallbackonfunctionexit"></a>IActiveScriptProfilerCallback::OnFunctionExit
通知探查器对象，脚本引擎已完成执行函数调用不是调用到文档对象模型 (DOM)。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnFunctionExit(  
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
 对于 DOM 调用，脚本引擎将调用[IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)而不是`IActiveScriptProfilerCallback::OnFunctionExit`。 这是由于大量的唯一方法和属性的数组。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)   
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)