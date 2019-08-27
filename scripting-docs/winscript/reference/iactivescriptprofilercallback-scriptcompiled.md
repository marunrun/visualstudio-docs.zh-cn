---
title: IActiveScriptProfilerCallback::ScriptCompiled | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.ScriptCompiled
apilocation:
- scrobj.dll
ms.assetid: 1bb8e9be-cbb1-4a61-b36c-805127a56ac7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a198667e7dc30969c32b556620b139d52f833543
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993230"
---
# <a name="iactivescriptprofilercallbackscriptcompiled"></a>IActiveScriptProfilerCallback::ScriptCompiled
通知探查器对象的脚本引擎编译脚本。 为编译每个脚本调用此方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ScriptCompiled(  
    [in] PROFILER_TOKEN scriptId,  
    [in] PROFILER_SCRIPT_TYPE type,  
    [in] IUnknown *pIDebugDocumentContext);  
```  
  
#### <a name="parameters"></a>参数  
 `scriptId`  
 [in]编译该脚本唯一 ID。 由脚本引擎分配此 ID。  
  
 `type`  
 [in]已编译的脚本的类型。 在中定义的值[PROFILER_SCRIPT_TYPE 枚举](../../winscript/reference/profiler-script-type-enumeration.md)。  
  
 `pIDebugDocumentContext`  
 [in]如果可用，一个指向`IUnknown`探查器必须查询接口[IDebugDocumentContext 接口](../../winscript/reference/idebugdocumentcontext-interface.md)指针。 否则，这将为 null。  
  
## <a name="return-value"></a>返回值  
 此方法的返回值是脚本引擎忽略。  
  
## <a name="remarks"></a>备注  
 仅当主机支持此功能，脚本引擎可以提供文档上下文。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)