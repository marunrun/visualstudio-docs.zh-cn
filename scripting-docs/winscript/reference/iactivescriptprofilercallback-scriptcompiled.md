---
title: IActiveScriptProfilerCallback：： ScriptCompiled |Microsoft Docs
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
ms.openlocfilehash: f7252134fc86bfd63b74a181b18327212a1b2dc1
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571658"
---
# <a name="iactivescriptprofilercallbackscriptcompiled"></a>IActiveScriptProfilerCallback::ScriptCompiled
通知探查器对象脚本引擎编译了脚本。 将为编译的每个脚本调用此方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ScriptCompiled(  
    [in] PROFILER_TOKEN scriptId,  
    [in] PROFILER_SCRIPT_TYPE type,  
    [in] IUnknown *pIDebugDocumentContext);  
```  
  
#### <a name="parameters"></a>参数  
 `scriptId`  
 中已编译的脚本的唯一 ID。 此 ID 由脚本引擎分配。  
  
 `type`  
 中已编译的脚本的类型。 这些值是在[PROFILER_SCRIPT_TYPE 枚举](../../winscript/reference/profiler-script-type-enumeration.md)中定义的。  
  
 `pIDebugDocumentContext`  
 中如果有，则为指向 `IUnknown` 接口的指针，探查器必须查询[IDebugDocumentContext 接口](../../winscript/reference/idebugdocumentcontext-interface.md)指针。 否则，此值将为 null。  
  
## <a name="return-value"></a>返回值  
 脚本引擎将忽略此方法的返回值。  
  
## <a name="remarks"></a>备注  
 脚本引擎只能提供此主机支持的文档上下文。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)