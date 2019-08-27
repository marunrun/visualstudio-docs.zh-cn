---
title: IActiveScriptProfilerControl::StopProfiling |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerControl.StopProfiling
apilocation:
- scrobj.dll
ms.assetid: 23b46ed6-a398-44c0-bc49-bf122e697cfe
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 750693db9aa809e6b3521f0312cebcf45d8d720d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993003"
---
# <a name="iactivescriptprofilercontrolstopprofiling"></a>IActiveScriptProfilerControl::StopProfiling
停止分析脚本引擎上。 此方法调用[IActiveScriptProfilerCallback::Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)探查器对象，然后将其释放。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT StopProfiling(  
    [in] HRESULT hrShutdownReason);  
```  
  
#### <a name="parameters"></a>参数  
 `hrShutdownReason`  
 [in]作为参数传递的 HRESULT [IActiveScriptProfilerCallback::Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)探查器对象的方法。  
  
## <a name="return-value"></a>返回值  
 返回一个 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|未启用分析。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl 接口](../../winscript/reference/iactivescriptprofilercontrol-interface.md)