---
title: IActiveScriptProfilerControl2：:P repareProfilerStop |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2::PrepareProfilerStop
ms.assetid: e43a63bc-c44f-44a8-9db4-29062b9e6a16
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 24d4d73e0263882ad028ea66d3fac5e24f3af9ba
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571441"
---
# <a name="iactivescriptprofilercontrol2prepareprofilerstop"></a>IActiveScriptProfilerControl2::PrepareProfilerStop
通知探查器你将停止分析所有适用的脚本引擎。 通过使用此方法，如果在停止分析时 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 正在运行，则可以获取完整的调用堆栈。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT PrepareProfilerStop();  
```  
  
#### <a name="parameters"></a>参数  
 方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 返回 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|未能启动分析。|  
|`S_FALSE`|当脚本未运行时，分析已停止。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|未启用事件探查。|  
  
## <a name="remarks"></a>备注  
 调用 `IActiveScriptProfilerControl2::PrepareProfilerStop` 确保发送调用堆栈中的函数事件。 在当前选项卡上的任何脚本引擎上停止分析之前，必须先调用此方法。可以为任何脚本引擎调用方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl2：： CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)    
 [IActiveScriptProfilerControl2 接口](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)