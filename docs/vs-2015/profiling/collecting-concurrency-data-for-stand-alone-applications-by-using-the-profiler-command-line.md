---
title: 使用探查器命令行收集独立应用程序的并发数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- concurrency profiling method
- profiling tools,concurrency method
ms.assetid: 0a2c6d8a-50b3-48aa-b617-9137b049d21e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7fac1c840d93c03b659e7934a82eb53895b60ede
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68141936"
---
# <a name="collecting-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line"></a>使用探查器命令行收集独立应用程序的并发数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具的并发方法可用于收集资源争用数据和线程活动数据，后者可显示 CPU 使用率、线程争用、线程迁移、同步延迟、重叠 IO 的区域和其他系统事件。  
  
## <a name="common-tasks"></a>常见任务  
  
|任务|相关的内容|  
|----------|---------------------|  
|**启动 .NET Framework 应用程序并分析并发数据**|-   [如何：启动 .NET Framework 的应用程序以收集并发数据](../profiling/how-to-launch-a-stand-alone-dotnet-framework-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line.md)|  
|**启动 C/C++ 应用程序并分析并发数据**|-   [如何：启动本机应用程序以收集并发数据](../profiling/how-to-launch-a-stand-alone-native-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line.md)|  
|**将探查器附加到正在运行的 .NET Framework 应用程序**|-   [如何：将探查器附加到 .NET Framework 的应用程序以收集并发数据](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line.md)|  
|**将探查器附加到正在运行的 C/C++ 应用程序**|-   [如何：将探查器附加到本机应用程序并收集并发数据](/visualstudio/profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data?view=vs-2015)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
### <a name="profiling-stand-alone-applications"></a>分析独立应用程序  
  
|任务|相关的内容|  
|----------|---------------------|  
|**使用采样方法进行分析**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application-by-using-the-profiler-command-line.md)|  
|**分析 .NET 内存分配和垃圾回收**|-   [收集 .NET Framework 内存数据](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**添加层交互数据**|-   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
  
### <a name="profiling-concurrency-issues"></a>分析并发问题  
  
|任务|相关的内容|  
|----------|---------------------|  
|**分析 ASP.NET 应用程序**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-an-aspnet-web-application-using-the-profiler-command-line.md)|  
|**分析服务**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|  
  
### <a name="analyzing-concurrency-data-views-and-reports"></a>分析并发数据视图和报告  
 [资源争用数据视图](../profiling/resource-contention-data-views.md)  
  
 [并发可视化工具](../profiling/concurrency-visualizer.md)  
  
## <a name="reference"></a>参考  
 [命令行分析工具引用](../profiling/command-line-profiling-tools-reference.md)
