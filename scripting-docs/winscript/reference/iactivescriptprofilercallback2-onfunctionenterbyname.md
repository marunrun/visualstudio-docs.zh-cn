---
title: IActiveScriptProfilerCallback2：： OnFunctionEnterByName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerCallback2::OnFunctionEnterByName
ms.assetid: 24b1593a-97fc-4d70-9b85-ec86fb59f987
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c0407441c77250b2cc27e9fee09c5039bb8e44ab
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571635"
---
# <a name="iactivescriptprofilercallback2onfunctionenterbyname"></a>IActiveScriptProfilerCallback2::OnFunctionEnterByName
通知探查器对象脚本引擎将执行文档对象模型（DOM）函数调用。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnFunctionEnterByName(  
    [in] [string] const WCHAR *pwszFunctionName,  
    [in] PROFILER_SCRIPT_TYPE scriptType);  
```  
  
#### <a name="parameters"></a>参数  
 `pwszFunctionName`  
 中脚本引擎将要执行的函数的名称。  
  
 `scriptType`  
 中函数的类型。 有关有效值的说明，请参阅[PROFILER_SCRIPT_TYPE 枚举](../../winscript/reference/profiler-script-type-enumeration.md)。  
  
## <a name="return-value"></a>返回值  
 脚本引擎将忽略此方法的返回值。  
  
## <a name="remarks"></a>备注  
 对于 DOM 调用，脚本引擎将调用此方法，而不是调用[IActiveScriptProfilerCallback：： OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)。 这是因为 DOM 中存在大量的唯一方法和属性。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)   
 [IActiveScriptProfilerCallback2 接口](../../winscript/reference/iactivescriptprofilercallback2-interface.md)