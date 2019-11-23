---
title: IActiveScriptProfilerControl2：： CompleteProfilerStart |Microsoft Docs
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
ms.openlocfilehash: f0230ecb480792b5b24b7375f5b95926735d0a61
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571554"
---
# <a name="iactivescriptprofilercontrol2completeprofilerstart"></a>IActiveScriptProfilerControl2::CompleteProfilerStart
通知探查器已开始分析所有适用的脚本引擎。 通过使用此方法，您可以在启动分析时，获取 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 正在运行的完整调用堆栈。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CompleteProfilerStart();  
```  
  
#### <a name="parameters"></a>参数  
 方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 返回 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|无法启动分析。|  
|`S_FALSE`|脚本未运行时启动了事件探查。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|未启用事件探查。 尚未设置回拨。|  
|`E_OUTOFMEMORY`|由于内存不足，无法获取调用堆栈。|  
  
## <a name="remarks"></a>备注  
 调用 `IActiveScriptProfilerControl2::CompleteProfilerStart` 确保发送已在调用堆栈中的函数事件。 在当前选项卡上的任何脚本引擎上启动分析后，必须调用此方法。可以为任何脚本引擎调用方法。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)   
 [IActiveScriptProfilerControl2 接口](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)