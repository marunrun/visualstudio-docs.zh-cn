---
title: IActiveScriptProfilerCallback2：： OnFunctionExitByName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerCallback2::OnFunctionExitByName
ms.assetid: a6ddead4-e66d-4789-b778-84e5c343f908
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a70bc72dd1070759ad8b78e43926f06a2c56ec15
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571617"
---
# <a name="iactivescriptprofilercallback2onfunctionexitbyname"></a>IActiveScriptProfilerCallback2::OnFunctionExitByName
通知探查器对象脚本引擎已完成运行文档对象模型（DOM）函数调用。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnFunctionExitByName(  
    [in] [string] const WCHAR *pwszFunctionName,  
    [in] PROFILER_SCRIPT_TYPE scriptType);  
  
```  
  
#### <a name="parameters"></a>参数  
 `pwszFunctionName`  
 中脚本引擎完成运行的函数的名称。  
  
 `scriptType`  
 中函数的类型。 有关有效值的说明，请参阅[PROFILER_SCRIPT_TYPE 枚举](../../winscript/reference/profiler-script-type-enumeration.md)。  
  
## <a name="return-value"></a>返回值  
 脚本引擎将忽略此方法的返回值。  
  
## <a name="remarks"></a>备注  
 对于 DOM 调用，脚本引擎将调用此方法，而不是调用[IActiveScriptProfilerCallback：： OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)。 这是因为 DOM 中存在大量的唯一方法和属性。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback2：： OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)    
 [IActiveScriptProfilerCallback2 接口](../../winscript/reference/iactivescriptprofilercallback2-interface.md)