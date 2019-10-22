---
title: IActiveScriptProfilerCallback：： Shutdown |Microsoft Docs
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
ms.openlocfilehash: deecfe4134a4b0e18591823f194ceaf6d1eb0a14
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571647"
---
# <a name="iactivescriptprofilercallbackshutdown"></a>IActiveScriptProfilerCallback::Shutdown
调用以通知探查器对象在脚本引擎上停止分析时的情况。 这样，探查器对象就可以根据需要调用其清理例程。 当脚本引擎关闭时，或者当对[IActiveScriptProfilerCallback：： Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)的调用失败时，此方法也由脚本引擎调用。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Shutdown(  
    [in] HRESULT hrReason);  
```  
  
#### <a name="parameters"></a>参数  
 `hrReason`  
 中关闭的原因。 如果脚本引擎正在关闭，则会传递 `S_OK`。 如果调用[IActiveScriptProfilerCallback：： Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)返回失败 hresult，则会传递 HRESULT。 否则，将从[IActiveScriptProfilerControl：： StopProfiling](../../winscript/reference/iactivescriptprofilercontrol-stopprofiling.md)检索此值。  
  
## <a name="return-value"></a>返回值  
 脚本引擎将忽略此方法的返回值。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)