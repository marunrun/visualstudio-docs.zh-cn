---
title: IActiveScriptProfilerCallback 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 76f9164b-b086-4b29-ac79-76f9c76f1d11
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9ae520dcb36e00dfaba8702db6294a5a47484b0a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571711"
---
# <a name="iactivescriptprofilercallback-interface"></a>IActiveScriptProfilerCallback 接口
提供当事件发生时脚本引擎用来通知探查器对象的方法。 此接口由探查器对象实现。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptProfilerCallback::Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)|调用以在脚本引擎上启动分析时初始化探查器对象。|  
|[IActiveScriptProfilerCallback::Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)|在脚本引擎上停止分析后，调用以释放探查器对象并释放探查器对象。|  
|[IActiveScriptProfilerCallback::ScriptCompiled](../../winscript/reference/iactivescriptprofilercallback-scriptcompiled.md)|向探查器对象通知脚本引擎编译了该脚本。|  
|[IActiveScriptProfilerCallback::FunctionCompiled](../../winscript/reference/iactivescriptprofilercallback-functioncompiled.md)|通知探查器对象脚本引擎在编译脚本时遇到了函数。|  
|[IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)|通知探查器对象：脚本引擎将要执行的函数调用不是对文档对象模型（DOM）的调用。|  
|[IActiveScriptProfilerCallback::OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)|通知探查器对象：脚本引擎已执行不是对 DOM 的调用的函数调用。|  
  
## <a name="remarks"></a>备注  
 对文档对象模型（DOM）的函数调用的通知由[IActiveScriptProfilerCallback2 接口](../../winscript/reference/iactivescriptprofilercallback2-interface.md)提供。  
  
> [!NOTE]
> 若要在脚本运行时添加启动和停止分析功能，请调用以下方法。 通过使用这些方法，如果在启动或停止分析时 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 正在运行，则可以获取完整的调用堆栈。  
> 
> - 调用[IActiveScriptProfilerControl2：： CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)以通知探查器已开始进行分析。  
>   - 调用[IActiveScriptProfilerControl2：:P repareprofilerstop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md) ，通知探查器你将很快停止分析。  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)