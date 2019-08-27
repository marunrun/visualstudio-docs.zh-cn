---
title: 阻塞时间分析报告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.blocking
helpviewer_keywords:
- Concurrency Visualizer, Blocking Time Profile Report
ms.assetid: 3bc45af0-3ba6-4fa3-a336-be8e9ae95107
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0efeb7fb0eb481d0b8d62ff4a9ebf9daad98c39f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147246"
---
# <a name="blocking-time-profile-report"></a>阻塞时间分析报告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分析报告提供特定于每个阻塞类别（例如，“I/O”或“同步”）的调用堆栈的合计阻塞时间数据。 优先报告列出抢占当前进程的进程以及抢占实例数。 为了生成阻塞分析报告，工具会收集阻塞 API 调用并将它们累计到调用堆栈树中。 这些报告中显示的数据因当前时间范围、隐藏线程和以下两个可能应用的筛选器而异：  
  
- 如果选择“仅我的代码”，则仅会显示具有用户代码的堆栈帧和该用户代码下的一个级别。  
  
- 如果设置了降噪值，则将跳过低于指定频率的排序堆栈。  
  
  展开所有调用树项，找到消耗阻塞时间的代码行。 若要找到某一项的源行，请在其快捷菜单上选择“查看源”  。 若要找到调用此项的代码行，请在快捷菜单上选择“查看调用站点”  。 如果只有一个调用站点可用，则此命令将连接到该调用站点的突出显示代码行。 如果有多个调用站点可用，则此命令将打开一个对话框，可选择其中一项，然后选择“转到源”  按钮以找到突出显示的调用站点。 在查看具有最多实例和/或最大时间的调用站点的源代码时，这往往最为有用。  
  
## <a name="blocking-time-report-columns"></a>阻塞时间报表列  
 下表显示每个阻塞时间报表的列。  
  
|列名称|说明|  
|-----------------|-----------------|  
|name|调用堆栈每个级别的函数的名称。|  
|实例数|可见时间段内阻塞调用的实例数。|  
|非独占阻塞时间|在上滚到此调用堆栈树级别的所有堆栈上所花费的总阻塞时间。 非独占数是此函数的独占阻塞时间及其所有子节点的独占阻塞时间的总和。|  
|独占阻塞时间|此函数处于最低调用堆栈级别期间所花费的总阻塞时间。 具有较高独占阻塞时间的唯一调用堆栈项可能是相关的函数。|  
|API/Wait 类别|仅对处于最低调用堆栈级别的函数显示。 如识别阻塞调用的签名，则将提供阻塞 API 的名称。 如果未识别签名，则提供内核所报告的信息。|  
|详细信息|该函数的完全限定名。 这包括行计数（如果有）。|  
  
### <a name="synchronization"></a>同步  
 同步报表显示对在同步上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅[同步时间](../profiling/synchronization-time.md)  
  
### <a name="sleep"></a>休眠  
 休眠报表显示对分配给休眠时间的阻塞时间的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅[休眠时间](../profiling/sleep-time.md)。  
  
### <a name="io"></a>I/O  
 I/O 报表显示对在 I/O 上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅 [I/O 时间（“线程”视图）](../profiling/i-o-time-threads-view.md)。  
  
### <a name="memory-management"></a>内存管理  
 内存管理报表显示对在内存管理操作上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅[内存管理时间](../profiling/memory-management-time.md)。  
  
### <a name="preemption"></a>优先  
 优先报告列出抢占当前进程的进程以及实例数。  您可以展开每个进程，查看当前进程中被替换的线程，以及按线程查看抢占实例的明细。 此阻塞报告的可操作性弱于其他报告，因为抢占通常是由操作系统施加于进程的，而不是由代码中的问题而施加。 有关详细信息，请参阅[抢占时间](../profiling/preemption-time.md)。  
  
### <a name="ui-processing"></a>UI 处理  
 UI 处理报表显示对在 UI 处理块上进行阻止的片段的调用，以及每个调用堆栈的合计阻塞时间。 有关详细信息，请参阅 [UI 处理时间](../profiling/ui-processing-time.md)。  
  
## <a name="see-also"></a>另请参阅  
 [线程视图](../profiling/threads-view-parallel-performance.md)
