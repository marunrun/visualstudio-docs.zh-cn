---
title: IActiveScriptProfilerControl2 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2 interface
ms.assetid: 89455276-5c23-420b-a7e0-804a32635291
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7059868ae65c5093b24f342bd303ec70172171c0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571530"
---
# <a name="iactivescriptprofilercontrol2-interface"></a>IActiveScriptProfilerControl2 接口
提供一些方法，这些方法可在脚本运行时添加启动或停止分析的功能。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)|通知探查器已开始分析所有适用的脚本引擎。 这使您可以在启动分析时，获取 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 正在运行的完整调用堆栈。|  
|[IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)|通知探查器你将停止分析所有适用的脚本引擎。 这使你可以获取完整的调用堆栈（如果在停止分析时 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 正在运行）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptProfilerControl 接口](../../winscript/reference/iactivescriptprofilercontrol-interface.md)   
 [Active Script Profiler 接口](../../winscript/reference/active-script-profiler-interfaces.md)