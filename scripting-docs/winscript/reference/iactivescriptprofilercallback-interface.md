---
title: IActiveScriptProfilerCallback Interface | Microsoft Docs
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
ms.openlocfilehash: e8f64f187638af7f9ab4bf6b80e88fe6992c78e6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386078"
---
# <a name="iactivescriptprofilercallback-interface"></a>IActiveScriptProfilerCallback 接口
提供脚本引擎用于发生事件时通知探查器对象的方法。 通过探查器对象来实现此接口。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptProfilerCallback::Initialize](../../winscript/reference/iactivescriptprofilercallback-initialize.md)|每当调用以初始化探查器对象对脚本引擎开始分析。|  
|[IActiveScriptProfilerCallback::Shutdown](../../winscript/reference/iactivescriptprofilercallback-shutdown.md)|调用以释放并释放探查器对象，只要在脚本引擎停止分析。|  
|[IActiveScriptProfilerCallback::ScriptCompiled](../../winscript/reference/iactivescriptprofilercallback-scriptcompiled.md)|通知探查器对象的脚本引擎编译该脚本。|  
|[IActiveScriptProfilerCallback::FunctionCompiled](../../winscript/reference/iactivescriptprofilercallback-functioncompiled.md)|通知探查器对象的脚本引擎编译脚本时遇到一个函数。|  
|[IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)|通知脚本引擎来执行不是到文档对象模型 (DOM) 的调用的函数调用的探查器对象。|  
|[IActiveScriptProfilerCallback::OnFunctionExit](../../winscript/reference/iactivescriptprofilercallback-onfunctionexit.md)|通知探查器对象，脚本引擎已完成执行函数调用不是对 DOM 的调用|  
  
## <a name="remarks"></a>备注  
 通过提供的函数调用到文档对象模型 (DOM) 的通知[IActiveScriptProfilerCallback2 接口](../../winscript/reference/iactivescriptprofilercallback2-interface.md)。  
  
> [!NOTE]
> 若要添加的功能来启动和停止分析运行脚本时，请调用以下方法。 通过使用这些方法，您可以获得完整的调用堆栈，如果[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]时启动或停止分析正在运行。  
> 
> - 调用[IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)通知探查器探查已经开始。  
>   - 调用[IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)通知探查器，您很快就会停止分析。  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)