---
title: 使用探查器命令行获取独立应用程序并发数据
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- concurrency profiling method
- profiling tools,concurrency method
ms.assetid: 0a2c6d8a-50b3-48aa-b617-9137b049d21e
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 15e8be092a8e1e065f2aa1a80be7447a370974b0
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331874"
---
# <a name="collect-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line"></a>使用探查器命令行收集独立应用程序的并发数据
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具的并发方法可用于收集资源争用数据和线程活动数据，后者可显示 CPU 使用率、线程争用、线程迁移、同步延迟、重叠 IO 的区域和其他系统事件。

## <a name="common-tasks"></a>常见任务

|任务|相关的内容|
|----------|---------------------|
|**启动 .NET Framework 应用程序并分析并发数据**|-   [如何：启动 .NET Framework 应用程序以收集并发数据](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-concurrency-data.md)|
|**启动 C/C++ 应用程序并分析并发数据**|-   [如何：启动本机应用程序以收集并发数据](../profiling/how-to-launch-a-stand-alone-native-application-to-collect-concurrency-data.md)|
|**将探查器附加到正在运行的 .NET Framework 应用程序**|-   [如何：将探查器附加到 .NET Framework 应用程序以收集并发数据](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-concurrency-data.md)|
|**将探查器附加到正在运行的 C/C++ 应用程序**|-   [如何：将探查器附加到本机应用程序中并收集并发数据](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data.md)|

## <a name="related-tasks"></a>相关任务

### <a name="profile-stand-alone-applications"></a>分析独立应用程序

|任务|相关的内容|
|----------|---------------------|
|**使用采样方法进行分析**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**分析 .NET 内存分配和垃圾回收**|-   [收集 .NET Framework 内存数据](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|
|**添加层交互数据**|-   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)|

### <a name="profile-concurrency-issues"></a>分析并发问题

|任务|相关的内容|
|----------|---------------------|
|**分析 ASP.NET 应用程序**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|
|**分析服务**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|

### <a name="analyze-concurrency-data-views-and-reports"></a>分析并发数据视图和报告
- [资源争用数据视图](../profiling/resource-contention-data-views.md)

- [并发可视化工具](../profiling/concurrency-visualizer.md)

## <a name="reference"></a>引用
- [命令行分析工具参考](../profiling/command-line-profiling-tools-reference.md)
