---
title: IActiveScriptProfilerControl：： StartProfiling |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerControl.StartProfiling
apilocation:
- scrobj.dll
ms.assetid: 56a7b3b7-8c21-43d0-9d8b-53bbc19fabb9
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b37b60f50351496faceb97190ae0d173eba3a5f4
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983261"
---
# <a name="iactivescriptprofilercontrolstartprofiling"></a>IActiveScriptProfilerControl::StartProfiling
开始分析脚本引擎。 脚本引擎通过调用[CoCreateInstance](/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)创建探查器对象的实例。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT StartProfiling(  
    [in] REFCLSID clsidProfilerObject,  
    [in] DWORD dwEventMask,  
    [in] DWORD dwContext);  
```  
  
#### <a name="parameters"></a>参数  
 `clsidProfilerObject`  
 中要创建的探查器对象的类标识符（CLSID）。  
  
 `dwEventMask`  
 中指定事件类型的4字节位掩码。 位在[PROFILER_EVENT_MASK 枚举](../../winscript/reference/profiler-event-mask-enumeration.md)中定义。  
  
 `dwContext`  
 中传递到探查器对象的4字节值。  
  
## <a name="return-value"></a>返回值  
 返回 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`ACTIVPROF_E_PROFILER_PRESENT`|已启用事件探查。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl 接口](../../winscript/reference/iactivescriptprofilercontrol-interface.md)