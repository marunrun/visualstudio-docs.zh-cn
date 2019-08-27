---
title: IActiveScriptProfilerControl2::CompleteProfilerStart | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2::CompleteProfilerStart
ms.assetid: e14d94a2-39d3-40a1-84d9-6300fbe2b339
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 36a1f5d6a1401e2860b65a29c8e383627e83c6be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993019"
---
# <a name="iactivescriptprofilercontrol2completeprofilerstart"></a>IActiveScriptProfilerControl2::CompleteProfilerStart
通知探查器在所有适用的脚本引擎探查已经开始。 通过使用此方法，您可以获得完整的调用堆栈，如果[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]时开始分析正在运行。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CompleteProfilerStart();  
```  
  
#### <a name="parameters"></a>参数  
 方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 返回一个 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|无法启动分析。|  
|`S_FALSE`|事件探查已启动时不运行脚本。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|未启用分析。 尚未设置不执行回调。|  
|`E_OUTOFMEMORY`|由于内存不足情况而无法获取调用堆栈。|  
  
## <a name="remarks"></a>备注  
 调用`IActiveScriptProfilerControl2::CompleteProfilerStart`可确保将发送事件的函数已在调用堆栈。 此方法必须分析上的当前选项卡上任何脚本引擎启动后调用。可以为任何脚本引擎调用该方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)   
 [IActiveScriptProfilerControl2 接口](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)