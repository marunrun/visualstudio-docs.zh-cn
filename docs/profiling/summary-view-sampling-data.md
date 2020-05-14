---
title: “摘要”视图 - 采样数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method, Summary view
- Summary view
ms.assetid: 79056873-2985-40be-9112-cdbc26a65156
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 649d0e9e5b32c124cfa962f45e4d128e4a32210f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778201"
---
# <a name="summary-view---sampling-data"></a>“摘要”视图 - 采样数据
“摘要”视图显示有关分析运行中性能开销最大的函数的信息。 有关详细信息（包括通知链接和报告列表的说明），请参阅[“摘要”视图](../profiling/summary-view.md)。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="timeline-graph"></a>时间线关系图
 “摘要”视图中的时间线关系图显示在进行分析的时间内分析的应用程序的处理器 (CPU) 利用率百分比。 可以使用时间线关系图将视图筛选到所选时间范围。 有关详细信息，请参阅[如何：从摘要时间线中筛选报告视图](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)。

## <a name="hot-path"></a>热路径
 “热路径”  显示在其中收集了最多样本的执行路径。 可以单击某个函数以显示该函数的“函数详细信息”视图。 若要显示函数的其他视图，请右键单击函数，然后单击列表中的视图。

 “热路径”  包含每个函数的以下数据：

|列|说明|
|------------|-----------------|
|**Name**|函数名。|
|**非独占样本数百分比**|此函数或此函数调用的函数执行时发生的样本占所有样本的百分比。|
|**独占样本数百分比**|此函数在函数体中执行代码时发生的样本占所有样本的百分比。 不包含此函数调用的函数中收集的样本。|

## <a name="functions-doing-most-individual-work"></a>执行单个工作最多的函数
 “执行单个工作最多的函数”  列表显示在分析运行中具有最大独占样本数的函数。 如果在收集样本时，某个函数在执行自己的代码，则向该函数分配独占样本。 如果在收集样本时，某个函数在调用其他函数，则不向该函数分配独占样本。 大量独占样本指示在函数本身中花费了大量时间。

 可以单击某个函数以显示该函数的“函数详细信息”视图。 若要显示函数的其他视图，请右键单击函数，然后单击列表中的视图。

 “执行单个工作最多的函数”  包含每个函数的以下数据：

|列|说明|
|------------|-----------------|
|**Name**|函数名。|
|**独占样本数百分比**|此函数在其函数体中执行代码时收集的样本数占分析运行中的所有样本数的百分比。 此百分比不包含在此函数调用的函数执行时收集的样本。|

## <a name="see-also"></a>另请参阅
- [“摘要”视图 - .NET 内存数据](../profiling/summary-view-dotnet-memory-data.md)
- [“摘要”视图 - 检测数据](../profiling/summary-view-instrumentation-data.md)
