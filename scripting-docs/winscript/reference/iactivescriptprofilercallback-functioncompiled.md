---
title: IActiveScriptProfilerCallback：： FunctionCompiled |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.FunctionCompiled
apilocation:
- scrobj.dll
ms.assetid: a7e9ef17-3891-4731-9d08-c37bc489be61
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a17ce7548a6524df6911cdf952393020472b88ed
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576473"
---
# <a name="iactivescriptprofilercallbackfunctioncompiled"></a>IActiveScriptProfilerCallback::FunctionCompiled
通知探查器对象脚本引擎在编译脚本时遇到了函数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT FunctionCompiled(  
    [in] PROFILER_TOKEN functionId,  
    [in] PROFILER_TOKEN scriptId,  
    [in] [string] const WCHAR *pwszFunctionName,  
    [in] [string] const WCHAR *pwszFunctionNameHint,  
    [in] IUnknown *pIDebugDocumentContext);  
```  
  
#### <a name="parameters"></a>参数  
 `functionId`  
 中函数的唯一 ID。 此 ID 由脚本引擎分配。  
  
 `scriptId`  
 中函数所属脚本的唯一 ID。  
  
 `pwszFunctionName`  
 中函数的名称，或者为 null （对于匿名函数）。  
  
 `pwszFunctionNameHint`  
 中推断函数的名称，如果脚本引擎不推断任何名称，则为 null。  
  
 `pIDebugDocumentContext`  
 中如果可用，指向探查器必须查询[IDebugDocumentContext 接口](../../winscript/reference/idebugdocumentcontext-interface.md)指针的 `IUnknown` 接口的指针。 否则为 null。  
  
## <a name="return-value"></a>返回值  
 脚本引擎将忽略此方法的返回值。  
  
## <a name="remarks"></a>备注  
 脚本引擎只能提供此主机支持的文档上下文。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)