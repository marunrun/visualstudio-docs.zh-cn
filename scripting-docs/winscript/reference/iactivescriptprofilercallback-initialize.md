---
title: IActiveScriptProfilerCallback：： Initialize |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerCallback.Initialize
apilocation:
- scrobj.dll
ms.assetid: a257111e-a50b-4962-9dd6-c893d40f6985
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bbbd61d6b3c10dcfffe2df215cc5a60d685dd803
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576446"
---
# <a name="iactivescriptprofilercallbackinitialize"></a>IActiveScriptProfilerCallback::Initialize
调用以在脚本引擎上启动分析时初始化探查器对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Initialize(  
    [in] DWORD dwContext);  
```  
  
#### <a name="parameters"></a>参数  
 `dwContext`  
 中传递给[IActiveScriptProfilerControl：： StartProfiling](../../winscript/reference/iactivescriptprofilercontrol-startprofiling.md)的4字节值。  
  
## <a name="return-value"></a>返回值  
 返回 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 如果该方法无法初始化探查器对象，则应返回失败 HRESULT 以通知脚本引擎。 在这种情况下，脚本引擎应直接调用[IActiveScriptProfilerCallback：： Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)，并在参数中传递 HRESULT，然后释放探查器对象。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)