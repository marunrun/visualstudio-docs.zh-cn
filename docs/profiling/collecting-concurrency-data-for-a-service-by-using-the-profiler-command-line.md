---
title: 使用探查器命令行获取服务的并发数据
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 275aacba-b2af-4d34-8931-ee30d777a256
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fba5c02846fa13cb0929a63e4007acb7db58535
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66262975"
---
# <a name="collect-concurrency-data-for-a-service-by-using-the-profiler-command-line"></a>使用探查器命令行收集服务的并发数据
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具的并发方法可用于收集资源争用数据和线程活动数据，后者可显示 CPU 使用率、线程争用、线程迁移、同步延迟、重叠 IO 的区域和其他系统事件。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|**附加到正在运行的 .NET 服务**|-   [如何：将探查器附加到 .NET 服务以收集并发数据](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-concurrency-data-by-using-the-command-line.md)|
|**添加层交互数据**|-   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)|
|**附加到正在运行的 C/C++ 服务**|-   [如何：将探查器附加到本机服务以收集并发数据](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line.md)|

## <a name="related-tasks"></a>相关任务

### <a name="profile-windows-services"></a>分析 Windows 服务

|任务|相关内容|
|----------|---------------------|
|**使用采样方法进行分析**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)|
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md)|
|**分析 .NET 内存分配和垃圾回收**|-   [收集 .NET 内存数据](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|

### <a name="profile-concurrency-data"></a>分析并发数据

|任务|相关内容|
|----------|---------------------|
|**分析独立应用程序**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)|
|**分析 ASP.NET Web 应用程序**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="analyze-concurrency-data-views-and-reports"></a>分析并发数据视图和报告
- [资源争用数据视图](../profiling/resource-contention-data-views.md)

- [并发可视化工具](../profiling/concurrency-visualizer.md)

## <a name="reference"></a>参考
- [命令行分析工具参考](../profiling/command-line-profiling-tools-reference.md)