---
title: “函数”视图 — 争用数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Functions view
ms.assetid: 208773b0-1a54-4b7a-ad37-2b6fd4f731d4
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1aaab824f40c0cd6ba0a240a6f3035d7ebcccd00
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68141894"
---
# <a name="functions-view---contention-data"></a>“函数”视图 - 争用数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

争用数据的“函数”报告视图列出了分析运行期间阻止执行的函数。  
  
 下表介绍了使用并发方法收集的分析数据文件的“函数”视图中显示的值。  
  
|列|说明|  
|------------|-----------------|  
|**独占阻塞的时间**|阻止此函数执行函数体内代码的时间。 不包含此函数调用的函数中的阻塞时间。|  
|**独占阻塞的时间百分比**|此函数的独占阻止时间占分析运行期间所有阻止时间的百分比。|  
|**独占争用**|阻止此函数执行函数体内代码的次数。 不包含该函数所调用的函数中的争用。|  
|**独占争用数百分比**|此函数的独占争用占分析运行中的所有争用的百分比。|  
|**函数地址**|函数的地址。|  
|**函数名**|该函数的完全限定名。|  
|**非独占阻塞的时间**|阻止此函数或此函数调用的函数执行的时间。|  
|**非独占阻塞的时间百分比**|此函数或模块的非独占阻止时间占分析运行期间所有阻止时间的百分比。|  
|**非独占争用**|阻止此函数或此函数调用的函数执行的次数。|  
|**非独占争用数百分比**|此函数或模块的非独占争用占分析运行期间所有争用的百分比。|  
|**函数行号**|此函数在源文件中的起始行号。|  
|**模块名**|函数所在模块的名称。|  
|**模块路径**|函数所在模块的路径。|  
|**进程 ID**|在其中执行模块的进程的进程 ID (PID)。|  
|**进程名**|进程的名称。|  
|**源文件**|此函数的定义所在的源文件。|  
  
## <a name="see-also"></a>另请参阅  
 [如何：自定义报告视图列](../profiling/how-to-customize-report-view-columns.md)   
 [“函数”视图](../profiling/functions-view.md)   
 [“函数”视图 - 检测](../profiling/functions-view-dotnet-memory-instrumentation-data.md)   
 [“函数”视图 - 采样](../profiling/functions-view-dotnet-memory-sampling-data.md)   
 [“函数”视图](../profiling/functions-view-instrumentation-data.md)   
 [“函数”视图](../profiling/functions-view-sampling-data.md)
