---
title: IActiveScriptProfilerControl 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1448b394-9743-41b5-8eb9-5026a45773a4
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ef127e3a4463d112b9ea424702fb2650c80cce7d
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571603"
---
# <a name="iactivescriptprofilercontrol-interface"></a>IActiveScriptProfilerControl 接口
由支持分析的脚本引擎实现。 通常，实现 `IActiveScriptProfilerControl` 的对象还实现[IActiveScript](../../winscript/reference/iactivescript.md)接口。 在这种情况下，您可以通过对对象调用 `IUnknown::QueryInterface` 方法来获取 `IActiveScriptProfilerControl` 接口的句柄。 接口提供了在脚本引擎上停止和启动分析所需的方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptProfilerControl::StartProfiling](../../winscript/reference/iactivescriptprofilercontrol-startprofiling.md)|开始分析脚本引擎。|  
|[IActiveScriptProfilerControl::SetProfilerEventMask](../../winscript/reference/iactivescriptprofilercontrol-setprofilereventmask.md)|设置脚本引擎中的探查器事件掩码。|  
|[IActiveScriptProfilerControl::StopProfiling](../../winscript/reference/iactivescriptprofilercontrol-stopprofiling.md)|停止对脚本引擎的分析。|  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)