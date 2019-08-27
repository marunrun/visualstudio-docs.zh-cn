---
title: IActiveScriptProfilerCallback2 Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerCallback2 interface
ms.assetid: 8f2e62e4-c232-4dc3-a2c0-54dd06298306
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b0a0df287db477c5bf768798f200ea0d97de6d1e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385946"
---
# <a name="iactivescriptprofilercallback2-interface"></a>IActiveScriptProfilerCallback2 接口
提供脚本引擎用于文档对象模型 (DOM) 的事件发生时通知探查器对象的方法。 通过探查器对象来实现此接口。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)|通知探查器对象的脚本引擎要运行 DOM 函数调用。|  
|[IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)|通知探查器的脚本引擎的对象完成运行 DOM 函数调用。|  
  
## <a name="remarks"></a>备注  
 `IActiveScriptProfilerCallback2` Internet Explorer 9 中首次发布的接口。  
  
 通知不是到 DOM 的调用的函数调用由[IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)。  
  
> [!NOTE]
> 若要添加的功能来启动和停止分析运行脚本时，请调用以下方法。 通过使用这些方法，您可以获得完整的调用堆栈，如果[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]时启动或停止分析正在运行。  
> 
> - 调用[IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)通知探查器探查已经开始。  
>   - 调用[IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)通知探查器，您很快就会停止分析。  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)