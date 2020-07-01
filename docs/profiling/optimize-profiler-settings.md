---
title: 优化探查器设置 | Microsoft Docs
ms.date: 4/29/2020
ms.topic: conceptual
helpviewer_keywords:
- Profiler, improve performance
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 9ff76364026230d08d03c91d14bddba3c325e7be
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290811"
---
# <a name="optimizing-profiler-settings"></a>优化探查器设置

Visual Studio 中的“性能探查器”和“诊断工具”窗口有许多不同的设置，这些设置会影响工具的总体性能。 更改某些设置可能会导致分析快速运行，也可能会在工具中处理结果时造成额外的等待时间。 下面汇总了特定设置及其对性能的影响。

## <a name="symbol-settings"></a>符号设置

调试程序选项中的符号设置（“调试”>“选项”>“符号”）对工具中生成结果所需的时间有显著影响。 启用符号服务器或使用 _NT_SYMBOL_PATH 会导致探查器为报表中加载的每个模块请求符号。 目前，探查器始终自动加载所有符号，而不管自动符号加载首选项是什么。

![符号加载页](../profiling/media/symbolloading.png "符号加载")

可以在“诊断工具”标题下的“输出”窗口中查看符号加载进度。

![符号加载进度](../profiling/media/symbolloadingprogress.png "符号加载进度")

下载后，符号就会进行缓存，这将加快以后的分析，但仍需要加载和分析文件。 如果符号加载减慢了分析速度，请尝试禁用符号服务器，并清除符号缓存。 转为依赖在本地为你的项目生成的符号。

## <a name="show-external-code"></a>显示外部代码

“性能探查器”和“诊断工具”窗口中的许多工具都有用户代码与外部代码的概念。 用户代码是由打开的解决方案或打开的工作区生成的任何代码。 外部代码就是除此以外的其他任何代码。 通过保持禁用“显示外部代码”设置，或保持启用“仅显示我的代码”，可以让工具将外部代码聚合到单一的一级框架中，从而大大减少显示结果所需的处理量。 这样，用户就可以查看外部代码中调用了什么导致速度变慢，同时将要处理的数据降到最低。 尽可能保持禁用“显示外部代码”，并确保已为正在分析的 diagsession 打开了解决方案或工作区。

## <a name="trace-duration"></a>跟踪持续时间

分析较短的持续时间会产生较少的数据，从而加快分析。 通常建议尝试将跟踪的性能数据限制为不超过五分钟。 使用某些工具（如 [CPU 使用情况](../profiling/cpu-usage.md)工具），可以在工具运行时暂停数据收集，这样你可以限制为只收集要分析的方案的数据量。

## <a name="sampling-frequency"></a>采样频率

使用某些工具（如 [CPU 使用情况](../profiling/cpu-usage.md)工具和 [NET 对象分配](../profiling/dotnet-alloc-tool.md)工具），可以调整采样频率。 增加此采样频率可以更精确地进行度量，但会增加生成的数据量。 通常，最好将此设置保持为默认频率，除非正在调查特定问题。

![诊断中心属性页](../profiling/media/diaghubpropertiespage.png "诊断中心属性页")

## <a name="see-also"></a>请参阅

- [运行带或不带调试程序的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
- [同时使用多个探查器工具](../profiling/use-multiple-profiler-tools-simultaneously.md)
- [了解性能收集方法](../profiling/understanding-performance-collection-methods-perf-profiler.md)
