---
title: IActiveScriptProfilerControl2::PrepareProfilerStop | Microsoft Docs
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
ms.openlocfilehash: 11a32f36ec6eddcc06faa77e093f19e8df503fa4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62968758"
---
# <a name="iactivescriptprofilercontrol2prepareprofilerstop"></a>IActiveScriptProfilerControl2::PrepareProfilerStop
通知探查器要停止分析在所有适用的脚本引擎。 通过使用此方法，您可以获得完整的调用堆栈，如果[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]时停止分析正在运行。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT PrepareProfilerStop();  
```  
  
#### <a name="parameters"></a>参数  
 方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 返回一个 HRESULT。 可能的值如下：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|无法启动分析。|  
|`S_FALSE`|分析已停止时不运行脚本。|  
|`ACTIVPROF_E_PROFILER_ABSENT`|未启用分析。|  
  
## <a name="remarks"></a>备注  
 调用`IActiveScriptProfilerControl2::PrepareProfilerStop`可确保将发送事件的调用堆栈中的函数。 此方法必须在调用之前停止在当前选项卡上的任何脚本引擎上进行分析。可以为任何脚本引擎调用该方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)   
 [IActiveScriptProfilerControl2 接口](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)