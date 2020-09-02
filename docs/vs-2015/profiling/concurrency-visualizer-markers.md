---
title: 并发可视化工具标记 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markersui
ms.assetid: c4692d17-6cd2-4ad1-8590-d7275c771c70
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 43b6115c45f9583b90711ef030834da662106f08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704354"
---
# <a name="concurrency-visualizer-markers"></a>并发可视化工具标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在并发可视化工具中，标记是代表应用事件的图标。  通常，应用生成这些事件是为了指定应用程序中的阶段或匹配项。  事件可以由应用或应用所使用的库和运行时生成。  
  
## <a name="kinds-of-markers"></a>标记类型  
 并发可视化工具使用三类标记来表示应用程序事件：标志、消息和跨度。  
  
1. *标志*用于指示应用中关注的时间点。  例如，您可以使用标记来表示一个达到特定阈值或引发异常的变量值。  
  
2. *消息*也标记时间点，但可以将其用于日志样式的跟踪。  例如，过去可能转储到日志文件的内容，现在可以包装到消息调用中，以便对其进行追踪并在并发可视化工具中查看。 还可以使用并发可视化工具将此数据导出到 CSV 文件。  
  
3. *范围*表示应用中的时间间隔，例如，它其中的某个阶段。  
  
## <a name="marker-linkage-to-threads"></a>线程的标记链接  
 每个生成标记的线程都有单独的时间线通道。  负责生成标记事件的线程的 ID 显示在标记通道的说明旁。  标记通道左侧显示的 ID 与当前进程中其他线程的 ID 匹配。  
  
## <a name="marker-importance"></a>标记重要性  
 标记可以有四种重要性级别：低，常规，高和重要。  您可以根据重要性级别筛选标记源。  例如，如果只想查看重要性为常规或重要的特定源中的标记，则可以在[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框中配置筛选器。标记的重要性显示在其工具提示和[标记报表](../profiling/markers-report.md)中。  
  
## <a name="marker-category"></a>标记类别  
 标记类别表示来自同一来源的一组标记事件。  并发可视化工具使用颜色来区分不同的标志和跨度类别。 您可以配置并发可视化工具，使之用类别来筛选来自特定事件提供程序的事件标记。  使用[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框以配置筛选器。  
  
## <a name="known-sources-of-markers"></a>已知的标记源  
 只要某些约束，任何 ETW 提供程序都可以生成标记。 您可以配置并发可视化工具，使之侦听其他的标记事件源。 默认情况下，它将侦听这些事件源：  
  
- [并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md)  
  
- [任务并行库 (TPL)](https://msdn.microsoft.com/library/b8f99f43-9104-45fd-9bff-385a20488a23)  
  
- [数据流](https://msdn.microsoft.com/library/643575d0-d26d-4c35-8de7-a9c403e97dd6)  
  
- [并行 LINQ (PLINQ)](https://msdn.microsoft.com/library/3d4d0cd3-bde4-490b-99e7-f4e41be96455)  
  
- [并发运行时](https://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c)  
  
- [方案标记支持](https://msdn.microsoft.com/e3b55bc2-b451-4214-ae00-0c7f5a5baec8)  
  
- [C++ AMP (C++ Accelerated Massive Parallelism)](https://msdn.microsoft.com/library/e27824cb-3167-409b-8c3f-a0e476d8f349)  
  
  使用[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框中的“标记”选项卡，可以控制是否在并发可视化工具中显示来自不同源的标记，也可以根据重要性和类别来筛选标记。  
  
## <a name="markers-from-eventsource"></a>来自 EventSource 的标记  
 并发可视化工具还可以显示 EventSource 事件。  有关详细信息，请参阅[将 EventSource 事件作为标记可视化](../profiling/visualizing-eventsource-events-as-markers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [标志标记](../profiling/flag-markers.md)   
 [消息标记](../profiling/message-markers.md)   
 [范围标记](../profiling/span-markers.md)   
 [将 EventSource 事件作为标记可视化](../profiling/visualizing-eventsource-events-as-markers.md)
