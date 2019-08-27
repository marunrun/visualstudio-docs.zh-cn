---
title: IActiveScriptProfilerControl::SetProfilerEventMask | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProfilerControl.SetProfilerEventMask
apilocation:
- scrobj.dll
ms.assetid: 207e192f-e12e-4fcb-b4d8-eaee50ecb86e
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 01e55d793d174f550e33e18558eccc19d417c80b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993085"
---
# <a name="iactivescriptprofilercontrolsetprofilereventmask"></a>IActiveScriptProfilerControl::SetProfilerEventMask
设置指定的脚本引擎应引发的事件类型的 4 字节位掩码。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetProfilerEventMask(  
    [in] DWORD dwEventMask);  
```  
  
#### <a name="parameters"></a>参数  
 `dwEventMask`  
 [in]4 字节位掩码，用于指定事件的类型。 在中定义 bits [PROFILER_EVENT_MASK 枚举](../../winscript/reference/profiler-event-mask-enumeration.md)。  
  
## <a name="return-value"></a>返回值  
 返回一个 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|未启用分析。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl 接口](../../winscript/reference/iactivescriptprofilercontrol-interface.md)