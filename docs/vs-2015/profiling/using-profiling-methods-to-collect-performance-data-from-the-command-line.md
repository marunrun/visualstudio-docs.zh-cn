---
title: 从命令行使用分析方法收集性能数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 5613fafc-f298-4e7a-9a2d-a853b61cdf9c
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6fe9e8d3dbd1e7395287cd7241f1e6145dffca7e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145402"
---
# <a name="using-profiling-methods-to-collect-performance-data-from-the-command-line"></a>从命令行使用分析方法收集性能数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

选择的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具命令行工具和选项取决于各种因素，如进行分析的应用程序的类型、要使用的分析方法以及是以本机还是 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 代码编码目标应用程序。  
  
 本主题根据选择的分析方法组织命令行过程主题。  
  
## <a name="in-this-topic"></a>在本主题中  
 [使用采样方法收集性能统计信息](#BKMK_Using_the_sampling_method_to_collect_performance_statistics)  
  
 [使用检测方法收集详细计时数据](#BKMK_Using_the_instrumentation_method_to_collect_detailed_timing_data)  
  
 [使用 .NET 内存方法收集内存分配数据和对象生存期数据](#BKMK_Using__NET_memory_methods_to_collect_memory_allocation_and_object_lifetime_data)  
  
 [使用并发方法收集资源争用数据和线程活动数据](#BKMK_Using_the_concurrency_method_to_collect_resource_contention_and_thread_activity_data)  
  
 [将层交互数据添加到分析运行](#BKMK_Adding_tier_interaction_data_to_a_profiling_run)  
  
## <a name="BKMK_Using_the_sampling_method_to_collect_performance_statistics"></a> 使用采样方法收集性能统计信息  
 分析工具采样方法在分析运行中按指定间隔收集性能数据。 采样数据可以提供对占用大量 CPU 的性能问题的深入了解，并且可以是开始探索应用程序性能的好办法。  
  
 可以同时启动探查器和应用程序，也可以将探查器附加到正在运行的应用程序实例。  
  
|任务|目标应用程序类型|  
|----------|-----------------------------|  
|**启动应用程序**|-   [独立应用程序](../profiling/how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line.md)|  
|**附加到正在运行的进程**|-   [.NET Framework 独立应用程序](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)<br />-   [本机独立应用程序](../profiling/how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)<br />-   [ASP.NET Web 应用程序](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [.NET 服务](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [本机服务](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line.md)|  
  
## <a name="BKMK_Using_the_instrumentation_method_to_collect_detailed_timing_data"></a> 使用检测方法收集详细计时数据  
 分析工具检测方法从包含软件探测的应用程序二进制文件副本收集性能数据，以记录性能信息。 会在每个检测的函数开始和结束时，以及在每次从检测的函数调用其他函数时收集检测数据。 检测方法可用于发现与 I/O 问题有关的性能问题（如磁盘使用率）。  
  
 可使用 [VInstr.exe](../profiling/vsinstr.md) 工具创建检测的二进制文件。 初始化探查器之后，会在运行目标应用程序时自动从检测的二进制文件收集数据。  
  
 **目标应用程序类型**  
  
- [.NET Framework 独立组件](../profiling/how-to-instrument-a-stand-alone-dotnet-framework-component-and-collect-timing-data-with-the-profiler-from-the-command-line.md)  
  
- [本机独立组件](../profiling/how-to-instrument-a-native-stand-alone-component-and-collect-timing-data-with-the-profiler-from-the-command-line.md)  
  
- [静态编译的 ASP.NET Web 应用程序](../profiling/how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line.md)  
  
- [动态编译的 ASP.NET Web 应用程序](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line.md)  
  
- [.NET 服务](../profiling/how-to-instrument-a-dotnet-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)  
  
- [本机服务](../profiling/how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)  
  
## <a name="BKMK_Using__NET_memory_methods_to_collect_memory_allocation_and_object_lifetime_data"></a> 使用 .NET 内存方法收集内存分配数据和对象生存期数据  
 分析工具 .NET 内存方法使你可以收集有关 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 中的对象生存期的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 内存分配数据和信息。  
  
 可以使用探查器启动目标应用程序；可以将探查器附加到正在运行的应用程序实例；并且可以创建应用程序的受检测版本以收集详细计时信息以及 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 内存数据。  
  
|任务|目标应用程序类型|  
|----------|-----------------------------|  
|**启动应用程序**|-   [独立 .NET Framework 应用程序](../profiling/how-to-launch-a-stand-alone-dotnet-framework-application-with-the-profiler-to-collect-memory-data-by-using-the-command-line.md)|  
|**附加到正在运行的进程**|-   [.NET Framework 独立应用程序](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-to-collect-memory-data-by-using-the-command-line.md)<br />-   [ASP.NET Web 应用程序](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)<br />-   [.NET 服务](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-memory-data-by-using-the-command-line.md)|  
|**检测模块**|-   [.NET Framework 独立组件](../profiling/how-to-instrument-a-stand-alone-dotnet-framework-component-and-collect-memory-data-with-the-profiler-by-using-the-command-line.md)<br />-   [静态编译的 ASP.NET Web 应用程序](../profiling/how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)<br />-   [动态编译的 ASP.NET Web 应用程序](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)<br />-   [.NET 服务](../profiling/how-to-instrument-a-dotnet-framework-service-and-collect-memory-data-by-using-the-profiler-command-line.md)|  
  
## <a name="BKMK_Using_the_concurrency_method_to_collect_resource_contention_and_thread_activity_data"></a> 使用并发方法收集资源争用数据和线程活动数据  
 分析工具并发方法使你可以从多线程应用程序收集资源争用以及线程和进程活动数据。  
  
 可以使用探查器启动应用程序，也可以将探查器附加到正在运行的应用程序实例。  
  
|任务|目标应用程序类型|  
|----------|-----------------------------|  
|**启动应用程序**|-   [独立 .NET Framework 应用程序](../profiling/how-to-launch-a-stand-alone-dotnet-framework-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [独立本机应用程序](../profiling/how-to-launch-a-stand-alone-native-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line.md)|  
|**附加到正在运行的进程**|-   [.NET Framework 独立应用程序](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [本机独立应用程序](/visualstudio/profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data?view=vs-2015)<br />-   [ASP.NET Web 应用程序](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [.NET 服务](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [本机服务](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line.md)|  
  
## <a name="BKMK_Adding_tier_interaction_data_to_a_profiling_run"></a> 将层交互数据添加到分析运行  
 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 请参阅[收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)  
  
## <a name="see-also"></a>另请参阅  
 [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [分析服务](../profiling/command-line-profiling-of-services.md)
