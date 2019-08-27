---
title: IActiveScriptProfilerCallback::Shutdown | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.Shutdown
apilocation:
- scrobj.dll
ms.assetid: 1281bf3c-d7d8-4ff5-9d8a-d1761fdb262e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 091ccc30f16081fdca8f10778efec208ef5ccb16
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993418"
---
# <a name="iactivescriptprofilercallbackshutdown"></a>IActiveScriptProfilerCallback::Shutdown
调用以通知探查器对象，只要在脚本引擎停止分析。 这样一来，如果需要，探查器对象可以调用其清理例程。 当脚本引擎正在关闭，或者当调用还通过脚本引擎调用此方法[IActiveScriptProfilerCallback::Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)失败。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Shutdown(  
    [in] HRESULT hrReason);  
```  
  
#### <a name="parameters"></a>参数  
 `hrReason`  
 [in]关闭原因。 如果脚本引擎正在关闭，`S_OK`传递。 如果在调用[IActiveScriptProfilerCallback::Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)返回失败 HRESULT，将 HRESULT 传递。 否则，此值检索从[IActiveScriptProfilerControl::StopProfiling](../../winscript/reference/iactivescriptprofilercontrol-stopprofiling.md)。  
  
## <a name="return-value"></a>返回值  
 此方法的返回值是脚本引擎忽略。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)