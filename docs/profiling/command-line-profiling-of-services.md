---
title: 服务的命令行分析 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling toos,services
- profiling services
ms.assetid: f0d62318-b0e8-49c6-9a30-9f7a6adef2f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fde17ace877d9c2fe0ce6c98a64963d82550c3ae
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63405684"
---
# <a name="command-line-profiling-of-services"></a>通过命令行分析服务
本部分介绍从命令行使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具收集 Windows 服务的性能数据的步骤和选项。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="common-tasks"></a>常见任务

| 任务 | 相关内容 |
| - | - |
| **收集应用程序统计信息：** 使用采样法收集性能统计信息。 对于分析 CPU 使用率问题以及了解应用程序的常规性能特征，采样数据十分有用。 | -   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md) |
| **收集详细计时信息：** 使用检测方法收集详细计时信息。 检测数据可用于分析 IO 问题和精细分析应用程序方案。 | -   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md) |
| **收集 .NET 内存数据：** 使用采样法或检测法收集显示分配对象的大小和数量的 .NET 内存分配数据。 还可以收集对象生存期数据，此数据显示在每次垃圾回收生成中回收的对象的大小和数量。 | -   [收集 .NET 内存数据](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md) |
| **收集并发数据：** 使用并发方法收集资源争用数据和线程活动数据，后者可显示 CPU 使用率、线程争用、线程迁移、同步延迟、重叠 IO 的区域和其他系统事件。 | -   [收集并发数据](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md) |
| **添加层交互数据：** 可以添加有关服务对 Microsoft [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] 数据库进行的同步 ADO.NET 调用的性能数据。 | -   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md) |

## <a name="related-tasks"></a>相关任务

|任务|相关内容|
|----------|---------------------|
|**分析独立（客户端）应用程序**|-   [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)|
|**分析 ASP.NET 应用程序**|-   [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)|