---
title: 使用探查器命令行获取 ASP.NET Web 应用程序内存数据
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .NET memory profiling method
- profiling tools,.NET memory method
ms.assetid: 57acf2b0-327a-4c0e-8078-ac2f6d99457d
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 9e8d9fde00a2390793ae8efe05b684e73caca321
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74773054"
---
# <a name="collect-memory-data-from-an-aspnet-web-application-by-using-the-profiler-command-line"></a>使用探查器命令行收集 ASP.NET Web 应用程序的内存数据
本部分介绍使用 VSPerfCmd  命令行工具收集 ASP.NET Web 应用程序的内存分配数据和对象生存期数据的过程和选项。

> [!NOTE]
> 使用 VSPerfCmd  工具可完全访问分析工具功能，包括暂停和继续分析，以及从处理器和 Windows 性能计数器收集其他数据。 如果不需要此功能，也可以使用 VSPerfASPNETCmd  命令行工具。 与 [VSPerfCmd](../profiling/vsperfcmd.md) 命令行工具相比，无需设置任何环境变量，也不需要重启计算机。 有关详细信息，请参阅[使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|将探查器附加到正在运行的 ASP.NET 应用程序 |-   [如何：将探查器附加到 ASP.NET Web 应用程序以收集内存数据](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)|
|检测静态编译的二进制文件 |-   [如何：检测静态编译的 ASP.NET 应用程序并收集内存数据](../profiling/how-to-instrument-a-statically-compiled-aspnet-app-and-collect-memory-data.md)|
|检测动态编译的二进制文件 |-   [如何：检测动态编译的 ASP.NET 应用程序并收集内存数据](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data.md)|

## <a name="related-tasks"></a>相关任务

### <a name="profile-aspnet-web-applications"></a>分析 ASP.NET Web 应用程序

|任务|相关内容|
|----------|---------------------|
|**使用采样方法进行分析**|-   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md)|
|**分析资源争用和线程活动**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="profile-net-framework-memory-data"></a>分析 .NET Framework 内存数据

|任务|相关内容|
|----------|---------------------|
|**分析独立（客户端）应用程序**|-   [收集 .NET Framework 内存数据](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|
|**分析服务**|-   [收集 .NET 内存数据](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|

### <a name="analyze-net-memory-data-views-and-reports"></a>分析 .NET 内存数据视图和报告
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)

## <a name="reference"></a>参考
- [命令行分析工具参考](../profiling/command-line-profiling-tools-reference.md)
