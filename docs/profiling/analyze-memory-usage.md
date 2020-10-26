---
title: 分析内存使用情况
ms.custom: seodec18
ms.date: 10/12/2020
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0262081489ec6e037a006649c3041baf02b32d58
ms.sourcegitcommit: 172aaf05596a9d8ded298b7b104569c1cce6160e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "92007219"
---
# <a name="analyze-memory-usage"></a>分析内存使用情况

可以使用多种工具查找内存泄漏和低效内存使用情况，例如集成了调试程序的“内存使用情况”诊断工具，或性能探查器中的工具（如 .NET 对象分配工具和事后分析“内存使用情况”工具）。

通过内存使用率工具可以拍摄托管和本机内存堆的一个或多个快照  。 可收集 .NET、ASP.NET、C++ 或混合模式（.NET 和本机）应用的快照。 “内存使用情况”工具可以在打开的 Visual Studio 项目和已安装的 Microsoft Store 应用上运行，也可以附加到正在运行的应用或进程。 无论是否进行调试，都可以运行“内存使用情况”工具。 有关详细信息，请参阅[运行带或不带调试器的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)。 在调试程序中，你可以打开和关闭内存分析，并查看按每个对象细分的内存使用情况。 可以在暂停执行时（例如在断点处）查看内存使用情况结果。

.NET 开发人员可以在[内存使用情况](../profiling/memory-usage.md)工具和 [.NET 对象分配工具](../profiling/dotnet-alloc-tool.md)之间进行选择。
- .NET 对象分配工具可帮助确定 .NET 代码中的分配模式和异常，并帮助确认垃圾回收的常见问题。 此工具仅作为事后分析工具运行。 可以在本地或远程计算机上运行此工具。
- “内存使用”工具可帮助识别内存泄漏，这在 .NET 应用中通常不常见。 如果需要在检查内存时使用调试器功能，如单步执行代码，则建议使用[集成了调试器的内存使用](../profiling/beginners-guide-to-performance-profiling.md)工具。

可 Windows 7 及更高版本中使用不带调试器的分析工具。 要运行带调试器的分析工具（“诊断工具”窗口），需具备 Windows 8 及更高版本。

## <a name="blogs-and-videos"></a>博客和视频

[调试时分析 CPU 和内存](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)

[Visual C++ 博客：Visual C++ 2015 中的内存分析](https://devblogs.microsoft.com/cppblog/memory-profiling-in-visual-c-2015/)

## <a name="see-also"></a>请参阅

- [分析不调试的内存使用情况](../profiling/memory-usage-without-debugging2.md)
- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
