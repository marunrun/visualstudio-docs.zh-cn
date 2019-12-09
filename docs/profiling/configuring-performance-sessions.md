---
title: 配置性能会话 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- common tasks, performance
- common tasks, profiling tools
- profiling tools, common tasks
- performance, gathering data
ms.assetid: e1c3ba41-ffca-4edf-9a7f-8a5a9244ef9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1bdf1c372ffcb3ad3a0ebf102827565853947e2b
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74777859"
---
# <a name="configure-performance-sessions"></a>配置性能会话
通过使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具，可以收集大量各种应用程序类型的性能数据。 本节演示如何使用性能会话的“性能向导”属性和目标二进制文件配置分析工具以收集你感兴趣的数据。 分析工具配置属性还可用来控制分析运行中收集的数据量。 有关详细信息，请参阅[控制数据收集](../profiling/controlling-data-collection.md)。

> [!NOTE]
> 在许多情况下，使用“性能向导”的默认属性是收集分析数据的一种有效方法。 有关详细信息，请参阅[性能分析初学者指南](../profiling/beginners-guide-to-performance-profiling.md)和[入门](../profiling/getting-started-with-performance-tools.md)。

## <a name="common-tasks"></a>常见任务

| 任务 | 相关内容 |
| - | - |
| **设置基本分析选项：** 应配置 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 以使用 Microsoft 符号服务器。 这可确保你有权访问当前版本的 Windows 符号，如函数和参数名称以及其他 Microsoft 应用程序。 启动分析会话前，还可以指定其他常规选项，如对分析工具和分析数据文件名的系统权限。 | -   [如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)<br />-   [如何：串行化符号信息](../profiling/how-to-serialize-symbol-information.md)<br />-   [如何：设置当前会话](../profiling/how-to-set-the-current-session.md)<br />-   [如何：设置权限](../profiling/how-to-set-permissions.md)<br />-   [如何：设置性能数据文件名选项](../profiling/how-to-set-performance-data-file-name-options.md) |
| **指定想要收集的数据：** 用于配置分析会话的过程取决于想要分析的目标应用程序类型和想要收集的性能数据类型。 | -   [如何：选择收集方法](../profiling/how-to-choose-collection-methods.md)<br />-   [通过使用采样收集性能统计信息](../profiling/collecting-performance-statistics-by-using-sampling.md)<br />-   [收集 .NET 内存分配和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [通过使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)<br />-   [如何：分析网页中的 JavaScript 代码](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [收集线程和进程并发数据](../profiling/collecting-thread-and-process-concurrency-data.md)<br />-   [收集其他性能数据](../profiling/collecting-additional-performance-data.md) |
| **设置高级配置选项：** 分析加载多个版本的公共语言运行时 (CLR) 的 .NET Framework 应用程序时，可以指定对哪个版本进行分析。 当性能会话中有多个 .exe 文件时，可以设置二进制文件的启动顺序。 | -   [如何：指定 .NET Framework 运行时](../profiling/how-to-specify-the-dotnet-framework-runtime.md)<br />-   [如何：指定要启动的二进制文件](../profiling/how-to-specify-the-binary-to-start.md) |

## <a name="related-sections"></a>相关章节
- [控制数据收集](../profiling/controlling-data-collection.md)

## <a name="see-also"></a>请参阅
- [性能资源管理器](../profiling/performance-explorer.md)
