---
title: 活动脚本 Profiler 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ab8a1f0d-393c-4d6a-94c1-d5b8aa76788c
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eeadf0de5563a4882c067960559414167e729173
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422234"
---
# <a name="active-script-profiler-interfaces"></a>活动脚本探查器接口
活动脚本 Profiler 接口使您能够接收来自分析事件[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]引擎。  
  
 Activprof.h 标头文件提供了本部分中列出的接口。  
  
## <a name="in-this-section"></a>本节内容  
 以下接口启用分析：  
  
- [IActiveScriptProfilerControl 接口](../../winscript/reference/iactivescriptprofilercontrol-interface.md)  
  
- [IActiveScriptProfilerControl2 接口](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)  
  
- [IActiveScriptProfilerControl3 接口](../../winscript/reference/iactivescriptprofilercontrol3-interface.md)  
  
- [IActiveScriptProfilerControl5 接口](../../winscript/reference/iactivescriptprofilercontrol5-interface.md)  
  
- [IActiveScriptProfilerCallback 接口](../../winscript/reference/iactivescriptprofilercallback-interface.md)  
  
- [IActiveScriptProfilerCallback2 接口](../../winscript/reference/iactivescriptprofilercallback2-interface.md)  
  
- [IActiveScriptProfilerCallback3 接口](../../winscript/reference/iactivescriptprofilercallback3-interface.md)  
  
- [IActiveScriptProfilerHeapEnum 接口](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)  
  
  以下部分列出了用于分析的枚举：  
  
- [活动脚本探查器常量、枚举和结构](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)  
  
> [!NOTE]
> Internet Explorer 8 中首次发布活动脚本 Profiler 接口。 `IActiveScriptProfilerControl2`和`IActiveScriptProfilerCallback2`Internet Explorer 9 中首次发布接口。 [IActiveScriptProfilerControl3 接口](../../winscript/reference/iactivescriptprofilercontrol3-interface.md)， [IActiveScriptProfilerCallback3 接口](../../winscript/reference/iactivescriptprofilercallback3-interface.md)，并[IActiveScriptProfilerHeapEnum 接口](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)的接口首次发布的 Internet Explorer 10。 [IActiveScriptProfilerControl5 接口](../../winscript/reference/iactivescriptprofilercontrol5-interface.md)使用 Internet Explorer 11 首次发布。  
>   
> 在 Internet Explorer 8 和 Internet Explorer 9，仅[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]语言使用这些接口以支持脚本性能分析。  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)