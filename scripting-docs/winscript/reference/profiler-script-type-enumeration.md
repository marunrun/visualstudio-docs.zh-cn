---
title: PROFILER_SCRIPT_TYPE 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PROFILER_SCRIPT_TYPE
apilocation:
- scrobj.dll
ms.assetid: 3ab6633a-6241-44f0-b837-14336f70c71e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ca90a566db422d75fefc44267ffe10504bb872ce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62816780"
---
# <a name="profilerscripttype-enumeration"></a>PROFILER_SCRIPT_TYPE 枚举
指定脚本的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum {  
    PROFILER_SCRIPT_TYPE_USER,  
    PROFILER_SCRIPT_TYPE_DYNAMIC,  
    PROFILER_SCRIPT_TYPE_NATIVE,  
    PROFILER_SCRIPT_TYPE_DOM  
} PROFILER_SCRIPT_TYPE;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|PROFILER_SCRIPT_TYPE_USER|指定用户编写脚本代码。|  
|PROFILER_SCRIPT_TYPE_DYNAMIC|指定在执行期间动态生成的脚本代码。|  
|PROFILER_SCRIPT_TYPE_NATIVE|指定本机函数和对象定义的脚本引擎的脚本类型。|  
|PROFILER_SCRIPT_TYPE_DOM|指定到 Internet Explorer 中，例如，调用文档对象模型 (DOM) 的调用`document.getElementById`方法。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本 Profiler 常量、 枚举和结构](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)   
 [IActiveScriptProfilerCallback::ScriptCompiled](../../winscript/reference/iactivescriptprofilercallback-scriptcompiled.md)   
 [IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)   
 [IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)