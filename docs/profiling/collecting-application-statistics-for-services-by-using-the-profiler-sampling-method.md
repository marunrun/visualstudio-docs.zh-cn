---
title: 使用探查器采样方法收集应用程序统计信息
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 07840ab2-3a92-4744-ac87-48b19e0ceecd
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 17217a51c58e1d30b6e6854ee9dbb0c1fb662a3a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779683"
---
# <a name="collect-application-statistics-for-services-by-using-the-profiler-sampling-method"></a>使用探查器采样方法收集服务的应用程序统计信息
本部分介绍从命令行使用采样方法收集 Windows 服务的性能统计信息的步骤和选项。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|**将探查器附加到 .NET 服务**|-   [如何：将探查器附加到 .NET 服务以收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-application-statistics-by-using-the-command-line.md)|
|**添加层交互数据**|-   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)|
|**将探查器附加到 C/C++ 服务**|-   [如何：将探查器附加到本机服务以收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line.md)|

## <a name="related-tasks"></a>相关任务

### <a name="profile-windows-services"></a>分析 Windows 服务

|任务|相关内容|
|----------|---------------------|
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md)|
|**分析 .NET 内存分配和垃圾回收**|-   [收集 .NET 内存数据](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|
|**分析资源争用和线程活动**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|

### <a name="profile-by-using-the-sampling-method"></a>使用采样方法进行分析

|任务|相关内容|
|----------|---------------------|
|**分析独立（客户端）应用程序**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|**分析 ASP.NET Web 应用程序**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|

### <a name="analyze-sampling-data-views-and-reports"></a>分析采样数据视图和报告
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
