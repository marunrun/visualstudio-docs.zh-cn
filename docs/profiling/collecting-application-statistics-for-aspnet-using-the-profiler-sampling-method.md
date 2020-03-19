---
title: 收集 ASP.NET Web 应用的统计信息 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, sampling method
- sampling profling method
ms.assetid: f8383ab1-eb49-4d3f-8608-d8b4d51a81be
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: a2cae807a8d833cf2653ea23616eeb819673229e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74773239"
---
# <a name="collect-statistics-for-aspnet-web-apps"></a>收集 ASP.NET Web 应用的统计信息

本部分介绍如下进程的步骤和选项：使用 **VSPerfASPNETCmd** 和 **VSPerfCmd** 命令行工具和采样分析方法收集 ASP.NET Web 应用程序的性能统计信息。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

> [!NOTE]
> 尽管使用 **VSPerfCmd** 工具可完全访问分析工具功能，包括暂停和继续分析，以及从处理器和 Windows 性能计数器收集其他数据，但在不需要此功能时应使用 **VSPerfASPNETCmd** 命令行工具。 使用独立探查器分析 ASP.NET 网站时，**VSPerfASPNETCmd** 命令行工具是首选工具。 与 [VSPerfCmd](../profiling/vsperfcmd.md) 命令行工具相比，无需设置任何环境变量，也不需要重启计算机。 有关详细信息，请参阅[使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|**将探查器附加到 ASP.NET 应用程序**|-   [如何：将探查器附加到 ASP.NET Web 应用程序以收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)|

## <a name="related-tasks"></a>相关任务

### <a name="profile-aspnet-web-applications"></a>分析 ASP.NET Web 应用程序

|任务|相关内容|
|----------|---------------------|
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md)|
|**分析内存分配和垃圾回收**|-   [收集内存数据](../profiling/collecting-memory-data-from-an-aspnet-web-application.md)|
|**分析资源争用和线程活动**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="sample-method"></a>采样方法

|任务|相关内容|
|----------|---------------------|
|**分析独立（客户端）应用程序**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|-   **分析服务**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)|

### <a name="analyze-sampling-data-views-and-reports"></a>分析采样数据视图和报告
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
