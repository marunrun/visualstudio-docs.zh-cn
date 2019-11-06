---
title: 从命令行分析独立应用程序 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profillng tools,stand-alone applications
- profling stand-alone applications
ms.assetid: a47f2bf2-186d-4120-bb79-34e2f3a1ee42
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a3bcc9dabbd325674e0731adaf4fcfb5b1abcbb
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189406"
---
# <a name="command-line-profiling-of-stand-alone-applications"></a>通过命令行分析独立应用程序
本部分介绍从命令行使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具收集独立（客户端）应用程序的性能数据的步骤和选项。

## <a name="common-tasks"></a>常见任务

| 任务 | 相关的内容 |
| - | - |
| **收集应用程序统计信息：** 使用采样法收集性能统计信息。 对于分析 CPU 使用率问题以及了解应用程序的常规性能特征，采样数据十分有用。 | -   [使用采样收集应用程序统计信息](../profiling/collecting-application-statistics-for-stand-alone-applications.md) |
| **收集详细计时信息：** 使用检测方法收集详细计时信息。 检测数据可用于分析 I/O 问题和精细分析应用程序方案。 | -   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md) |
| **收集 .NET 内存数据：** 使用采样法或检测法收集显示分配对象的大小和数量的 .NET 内存分配数据。 还可以收集对象生存期数据，此数据显示在每次垃圾回收生成中回收的对象的大小和数量。 | -   [收集 .NET Framework 内存数据](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md) |
| **收集并发数据：** 使用并发方法收集资源争用数据和线程活动数据，后者可显示 CPU 使用率、线程争用、线程迁移、同步延迟、重叠 I/O 的区域和其他系统事件。 | -   [收集并发数据](../profiling/collecting-concurrency-data-for-stand-alone-applications.md) |
| **添加层交互数据：** 可以添加有关应用程序对 Microsoft [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] 数据库进行的同步 ADO.NET 调用的性能数据。 若要将层交互数据添加到分析运行，需要使用命令行分析工具执行特定的步骤。 | -   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md) |
| **尝试一下：** 使用分布过程以通过采样或检测方法分析示例客户端应用程序。 | -   [演练：使用采样进行命令行分析](../profiling/walkthrough-command-line-profiling-using-sampling.md)<br />-   [演练：使用检测进行命令行分析](command-line-profiling-of-stand-alone-applications.md) |

## <a name="related-tasks"></a>相关任务

|任务|相关内容|
|----------|---------------------|
|**分析 ASP.NET 应用程序**|-   [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)|
|**分析服务**|-   [分析服务](../profiling/command-line-profiling-of-services.md)|