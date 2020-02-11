---
title: 分析内存使用情况
ms.custom: seodec18
ms.date: 01/02/2018
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 98382cdcde1e8413d7b6592b52aaee09e6c4274c
ms.sourcegitcommit: 4be64917e4224fd1fb27ba527465fca422bc7d62
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76923336"
---
# <a name="analyze-memory-usage"></a>分析内存使用情况
使用集成了调试器的内存使用率  诊断工具，查找内存泄漏和低效内存使用的情况。 通过内存使用率工具可以拍摄托管和本机内存堆的一个或多个快照  。 可收集 .NET、ASP.NET、本机或混合模式（.NET 和本机）应用的快照。

- 你可以分析单个快照以了解有关内存使用的对象类型的相对影响，并在你的应用中查找低效使用内存的代码。

- 你还可以比较 (diff) 一个应用的两个快照，以便在你的代码中查找导致内存使用随时间增加的区域。

有关详细说明，请参阅[分析内存使用率](../profiling/memory-usage.md)教程。  目前，必须使用随附调试器的工具，才能度量 .NET Core 应用的内存使用情况。 对于其他托管应用和本机应用，可使用随附或未随附调试器的工具。

可 Windows 7 及更高版本中使用不带调试器的分析工具。 要运行带调试器的分析工具（“诊断工具”窗口），需具备 Windows 8 及更高版本  。

## <a name="blogs-and-videos"></a>博客和视频

[调试时分析 CPU 和内存](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)

[Visual C++ 博客：Visual C++ 2015 中的内存分析](https://devblogs.microsoft.com/cppblog/memory-profiling-in-visual-c-2015/)

## <a name="see-also"></a>请参阅

- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
- [分析不调试的内存使用情况](../profiling/memory-usage-without-debugging2.md)
