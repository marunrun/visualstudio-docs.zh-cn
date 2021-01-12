---
title: 将 dotnet 计数器可视化 | Microsoft Docs
description: 了解如何在 Visual Studio 性能探查器中使用 .NET 计数器工具。
ms.date: 12/7/2020
ms.topic: conceptual
helpviewer_keywords:
- dotnet, counters, profiling
author: sagar-shetty
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 7a09cc073b2886ab0d374bccaf8b85f3bb729dd7
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97905060"
---
# <a name="visualize-dotnet-counters-from-the-visual-studio-profiler"></a>从 Visual Studio 探查器中将 dotnet 计数器可视化


.NET 计数器工具允许你在 Visual Studio 探查器中随着时间将 [dotnet 计数器](/dotnet/core/diagnostics/dotnet-counters)可视化。


> [!NOTE]
> .NET 计数器工具需要 Visual Studio 2019 版本 16.7 或更高版本，并面向 .NET Core 3.0+。

## <a name="setup"></a>设置

1. 在 Visual Studio 中打开性能探查器（Alt+F2 或“调试”->“性能探查器”） 。

2. 选择“.NET 计数器”复选框。

   :::image type="content" source="../profiling/media/dotnet-counters-tool-selected.png" alt-text="已选中计数器工具。":::

3. 单击“启动”按钮，运行该工具。

有关如何优化工具性能的详细信息，请参阅[优化探查器设置](../profiling/optimize-profiler-settings.md)。


## <a name="understand-your-data"></a>了解数据

当该工具最初收集数据时，你可以看到 [dotnet 计数器](/dotnet/core/diagnostics/dotnet-counters)的实时值。

:::image type="content" source="../profiling/media/dotnet-counters-tool-collecting.png" alt-text=".NET 计数器工具正在收集数据。":::

还可以通过选中计数器名称旁边的复选框来查看计数器的图形。 一次可显示多个计数器的图形。


完成应用的运行和数据收集后，就可以停止为获取更详细的报表而执行的数据收集。 为此，请按“停止收集”按钮。


加载报表后，你应可看到一个与下面所示类似的最终报表。

:::image type="content" source="../profiling/media/dotnet-counters-tool-report.png" alt-text=".NET 计数器工具报表。":::

该报表将显示以下值：

- Min - 所选时间范围内该计数器的最小值。
- Max - 所选时间范围内该计数器的最大值。
- Average - 所选时间范围内该计数器的平均值。

通过右键单击列标题并选择一个标题，可以在表中筛选或添加列。

:::image type="content" source="../profiling/media/dotnet-counters-tool-columns.png" alt-text=".NET 计数器工具列。":::

还可以通过选中计数器旁边的复选框来查看详细报表中的图形。 默认情况下，表中的数据表示所收集跟踪的整个持续时间的值。 若要将数据筛选到特定的时间范围，请单击并拖动图形。

:::image type="content" source="../profiling/media/dotnet-counters-tool-time-filtering.png" alt-text=".NET 计数器工具时间筛选。":::

该表将更新为图形中所选时间的相关值。 使用“清除选定内容”按钮，将所选时间范围重置为整个跟踪。


## <a name="see-also"></a>请参阅

- [优化探查器设置](../profiling/optimize-profiler-settings.md)
- [dotnet 计数器](/dotnet/core/diagnostics/dotnet-counters)
