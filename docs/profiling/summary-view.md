---
title: “摘要”视图 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.summary
helpviewer_keywords:
- performance reports, summary view
- profiling tools reports, Summary view
- profiling tools, Summary view
- Summary view
ms.assetid: 98a1eb71-bbf5-4ce7-8559-cdc29f082c4b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66d44ff0c2c2406e9ba4508c835deab571b70e44
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926498"
---
# <a name="summary-view"></a>“摘要”视图
“摘要”视图显示有关分析运行期间，性能开销最大的函数或对象的信息。 此视图根据分析方法的性能指标，提供一个时间线图，以及性能开销最大的函数或对象的两个或多个列表。 此视图中的数据取决于所用的分析方法（采样、检测或并发）以及是否收集 .NET 内存分配。

 对于除并发数据的“摘要”视图以外的所有“摘要”视图，“摘要”视图中的时间线图显示被分析的应用程序在进行分析的这段时间内的处理器 (CPU) 使用率。

- 如果在图表上指定一个时间段，则可以重新分析该时间段的数据或缩放时间线以显示指定的时间段。 有关详细信息，请参阅[如何：从摘要时间线中筛选报表视图](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)。

- 可在“摘要”视图列表中单击函数，打开函数的“函数详细信息”视图。 还可右键单击函数获取其他视图选项。

- 若要修改在“摘要”视图列表中显示的项目数量，请打开“工具”  菜单，指向“选项”  ，然后单击“性能工具”  。 在“常规设置”  下，修改“‘摘要’视图中的函数数目”  设置。

## <a name="notifications-links"></a>通知链接
 可单击通知列表中的链接为报告设置显示选项。 列表位于时间线图的右侧。

|||
|-|-|
|**显示非用户代码**<br /><br /> **仅显示我的代码**|不可用于本机代码或分析数据（使用检测方法收集）。 在仅显示用户代码中的数据（“仅显示我的代码”  ）与显示包括系统代码在内的所有代码中的数据（“显示非用户代码”  ）之间切换。 默认情况下，数据仅限于用户代码。 要更改该设置，请参阅[如何：筛选分析工具报表视图以显示“仅我的代码”](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md)。|
|**视图指南**|在“错误列表”  窗口中显示性能规则警告。 有关详细信息，请参阅[使用性能规则对数据进行分析](../profiling/using-performance-rules-to-analyze-data.md)|

## <a name="report"></a>报告
 可单击报告列表中的链接，打开不同的视图并比较、保存或筛选报告。 列表位于时间线图的右侧。

| | |
|----------------------------| - |
| **显示已修整的调用树** | 在“调用树”视图中，显示性能开销最大的的执行路径。 有关详细信息，请参阅[“调用树”视图](../profiling/call-tree-view.md)。 |
| **显示热行** | 不可用于使用检测方法收集的分析数据。 在“行”视图中，显示性能开销最大的源代码行。 有关详细信息，请参阅[“行”视图](../profiling/lines-view.md)。 |
| **比较报告** | 显示“选择要比较的分析文件”  对话框，可在其中指定要与当前文件进行比较的另一个分析数据文件。 有关详细信息，请参阅[比较性能数据文件](../profiling/comparing-performance-data-files.md)。 |
| **导出报告数据** | 显示“导出报告”  对话框，可在其中指定一个或多个要保存为逗号分隔值 (.csv) 文件或 .xml 文件的报告视图。 有关详细信息，请参阅[如何：导出分析工具报表](/previous-versions/visualstudio/visual-studio-2010/ms182394\(v\=vs.100\))。 |
| **保存已分析的报告** | 将当前分析数据文件保存为 .vsps 文件，该文件可在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 界面中更快速地打开。 有关详细信息，请参阅[如何：保存已分析的数据文件](/previous-versions/visualstudio/visual-studio-2010/bb763106\(v\=vs.100\))。 |
| **筛选报告数据** | 显示分析报告筛选器窗格，可在其中指定条件来限制报告视图中显示的数据。 有关详细信息，请参阅[性能报告视图筛选器](../profiling/performance-report-view-filter.md) |
| **切换全屏显示** | 切换报告视图的全屏模式。 |

## <a name="see-also"></a>请参阅
- [“摘要”视图 - 采样数据](../profiling/summary-view-sampling-data.md)
- [“摘要”视图 - 检测数据](../profiling/summary-view-instrumentation-data.md)
- [“摘要”视图 - .NET 内存数据](../profiling/summary-view-dotnet-memory-data.md)