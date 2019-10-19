---
title: IActiveScriptProfilerCallback2 接口 |Microsoft Docs
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
ms.openlocfilehash: 25f9616497192659df67feedfe16bd9ea0c5e3b1
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577303"
---
# <a name="iactivescriptprofilercallback2-interface"></a>IActiveScriptProfilerCallback2 接口
提供在文档对象模型（DOM）事件发生时脚本引擎用来通知探查器对象的方法。 此接口由探查器对象实现。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptProfilerCallback2::OnFunctionEnterByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionenterbyname.md)|通知探查器对象脚本引擎将要运行 DOM 函数调用。|  
|[IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)|通知探查器对象：脚本引擎已完成 DOM 函数调用的运行。|  
  
## <a name="remarks"></a>备注  
 @No__t_0 接口首次与 Internet Explorer 9 一起发布。  
  
 不调用 DOM 的函数调用的通知由[IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)提供。  
  
> [!NOTE]
> 若要在脚本运行时添加启动和停止分析功能，请调用以下方法。 通过使用这些方法，如果在启动或停止分析时 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 正在运行，则可以获取完整的调用堆栈。  
> 
> - 调用[IActiveScriptProfilerControl2：： CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)以通知探查器已开始进行分析。  
>   - 调用[IActiveScriptProfilerControl2：:P repareprofilerstop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md) ，通知探查器你将很快停止分析。  
  
## <a name="see-also"></a>请参阅  
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)