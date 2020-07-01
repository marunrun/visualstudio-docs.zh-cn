---
title: 事件查看器 | Microsoft Docs
ms.date: 4/30/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, Events Viewer
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 4cba043d8300d47ae5ffba1c175a19fcfa2e65ed
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330330"
---
# <a name="events-viewer"></a>事件查看器

通用事件查看器通过一系列事件（如模块加载、线程启动和系统配置）显示应用活动。 此视图有助于在 Visual Studio 探查器中更好地诊断应用的运行情况。

## <a name="setup"></a>安装

1. 在 Visual Studio 中，按 Alt+F2 打开性能探查器。

1. 选中“事件查看器”复选框。

   ![已选中“事件查看器”复选框](../profiling/media/eventsviewerselected.png "已选中“事件查看器”复选框")

1. 选择“开始”按钮，以运行此工具。

1. 在此工具开始运行后，在应用中完成要探查的方案。 然后，选择“停止收集”或关闭应用，以查看数据。

   ![显示“停止收集”的窗口](../profiling/media/stopcollectioneventsviewer.png "显示“停止收集”的窗口")

若要详细了解如何提高此工具的效率，请参阅[优化分析设置](../profiling/optimize-profiler-settings.md)。

## <a name="understand-your-data"></a>了解数据

![事件查看器跟踪](../profiling/media/eventviewertrace.png "事件查看器跟踪")

|列名称|描述|
|----------|---------------------|
|提供商名称|事件源|
|事件名称|由其提供程序指定的事件|
|Text|事件的提供程序、事件名称和 ID 的说明|
|时间戳（毫秒）|事件发生的时间|
|提供程序 GUID|事件提供程序的 ID|
|事件 ID|事件的 ID|
|进程 ID|发生事件所在的进程（如果已知）|
|进程名|当前正在运行的进程的名称|
|线程 ID|发生事件所在的线程的 ID（如果已知）|

如果默认情况下缺少任何列，请右键单击现有列标题之一，然后选择要添加的列。

![向事件查看器添加列](../profiling/media/eventvieweraddcolumns.png "向事件查看器添加列")

选择事件后，就会看到“其他属性”窗口。 “通用属性”列出了将会为所有事件显示的属性。 “有效负载属性”显示了特定于事件的属性。 对于某些事件，还可以查看“堆栈”。

![显示堆栈的事件查看器](../profiling/media/eventviewerstacks.png "显示堆栈的事件查看器")

## <a name="organize-your-data"></a>整理数据

除了“文本”列以外的其他所有列都是可排序的。

![事件查看器跟踪](../profiling/media/eventviewertrace.png "事件查看器跟踪")

事件查看器一次最多可显示 20,000 个事件。 若要专注于相关事件，可以通过选择事件筛选器来筛选显示的事件。 还可以查看每个提供程序发生的事件总数所占的百分比。 如果将鼠标悬停在一个事件筛选器上，就能看到显示以下内容的工具提示：

- 事件名称
- 提供程序
- GUID
- 事件总数所占的百分比
- 事件计数

![事件查看器事件筛选器](../profiling/media/eventviewereventfilter.png "事件查看器事件筛选器")

提供程序筛选器显示了每个提供程序发生的事件总数所占的百分比。 如果将鼠标悬停在一个提供程序上，可以看到显示提供程序名称、事件总数所占百分比和事件计数的类似工具提示。

![事件查看器提供程序筛选器](../profiling/media/eventviewerproviderfilter.png "事件查看器提供程序筛选器")
