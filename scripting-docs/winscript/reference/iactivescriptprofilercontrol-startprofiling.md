---
title: IActiveScriptProfilerControl::StartProfiling |Microsoft Docs
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
ms.openlocfilehash: 780886e4ca21abbe11580992244cee0d6a28b134
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993132"
---
# <a name="iactivescriptprofilercontrolstartprofiling"></a>IActiveScriptProfilerControl::StartProfiling
启动脚本引擎的分析。 脚本引擎通过调用创建探查器对象的实例[CoCreateInstance](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT StartProfiling(  
    [in] REFCLSID clsidProfilerObject,  
    [in] DWORD dwEventMask,  
    [in] DWORD dwContext);  
```  
  
#### <a name="parameters"></a>参数  
 `clsidProfilerObject`  
 [in]类标识符 (CLSID) 要创建的探查器对象。  
  
 `dwEventMask`  
 [in]4 字节位掩码，用于指定事件的类型。 在中定义 bits [PROFILER_EVENT_MASK 枚举](../../winscript/reference/profiler-event-mask-enumeration.md)。  
  
 `dwContext`  
 [in]一个 4 字节值，该值传递给探查器对象。  
  
## <a name="return-value"></a>返回值  
 返回一个 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`ACTIVPROF_E_PROFILER_PRESENT`|已启用分析。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl 接口](../../winscript/reference/iactivescriptprofilercontrol-interface.md)