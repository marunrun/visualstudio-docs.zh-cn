---
title: 负载测试结果摘要概述
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.summary.view
helpviewer_keywords:
- load test results, summary
- load tests, summary in analyzer
- load tests, results summary
- Load Test Viewer, summary
- load tests, summary in Load Test Viewer
ms.assetid: 326b6c3c-5378-452b-8ca3-ba5a06ab3d41
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba72bc9d4e63e1ccb1e6d8c05d20332880e19ea9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652995"
---
# <a name="load-test-results-summary-overview"></a>负载测试结果摘要概述

运行负载测试后，可以查看负载测试摘要以快速了解结果。 负载测试摘要以简洁、易读的格式提供关键结果。 您还可以打印负载测试摘要， 以便于在向利益干系人传达结果时使用。 当您从以前运行的负载测试打开负载测试结果时，负载测试摘要也是默认视图。 有关详细信息，请参阅[如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)。

![“摘要”视图](../test/media/ltest_summaryview.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="the-load-test-summary"></a>负载测试摘要

负载测试摘要分为几个小节。 开头几节显示在摘要的顶部，并且始终可见。 当您查看负载测试摘要时，首先会看到下列各项：

- 有关测试运行的信息

- 整体结果

- 关键统计信息：最慢的前 5 个页面

- 关键统计信息：最慢的前 5 个测试

- 关键统计信息：最慢的前 5 个 SQL 操作

    > [!NOTE]
    > 只有在负载测试中启用了 SQL 跟踪的情况下，才会显示“SQL 操作”一节。

结尾几节出现在摘要的最后，可以折叠起来以节省空间。 下列各项出现在负载测试摘要的结尾：

- 测试结果

- 页结果

- 事务结果

- 测试中系统的资源

- 控制器和代理资源

- 错误

## <a name="test-run-information"></a>测试运行信息

“有关测试运行的信息”一节包含有关运行的一般信息，包括测试的名称、开始时间和结束时间以及运行测试的控制器。 此节还包含有关运行的可选说明，这些说明是您在运行负载测试时添加的。

## <a name="overall-results"></a>整体结果

“整体结果”一节包含测试的摘要结果，包括每秒钟的请求数、失败请求的总数、平均响应时间以及平均页面时间。

## <a name="key-statistic-top-5-slowest-pages"></a>关键统计信息：最慢的前 5 个页面

“最慢的页面”一节包含负载测试中最慢的 5 个页面。 此节显示每个页面的 URL 和平均页面加载时间。 这些页面按降序列出。 可选择某个页面的 URL 以打开“页”表和查看该页面的更多详细信息  。 有关详细信息，请参阅[如何：查看网页响应](../test/how-to-view-web-page-response-time-in-a-load-test.md)。

“95% 页面时间(秒)”的百分比值报告，95% 的页面在此时间内完成（以秒为单位）  。

## <a name="key-statistic-top-5-slowest-tests"></a>关键统计信息：最慢的前 5 个测试

“最慢的测试”一节包含负载测试中最慢的 5 个测试。 此节显示每个测试的测试名称和平均测试时间。 这些测试按降序列出。 可选择某个测试的名称以打开“测试”表和查看该测试的更多详细信息  。 有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

“95% 测试时间(秒)”的百分比值报告，95% 的测试在此时间内完成（以秒为单位）  。

## <a name="key-statistic-top-5-slowest-sql-operations"></a>关键统计信息：最慢的前 5 个 SQL 操作

如果在负载测试中启用了 SQL 跟踪，“最慢的查询”一节将包含负载测试中最慢的 5 个查询。 此节显示每个测试的操作名称和持续时间。 持续时间以微秒 (SQL Server 2005) 或毫秒（SQL Server 2000 和更低版本）显示。 这些测试按持续时间以降序列出。 可选择某个操作的名称以打开“SQL 跟踪”表，并查看该操作的更多详细信息  。 有关详细信息，请参阅 [SQL 跟踪数据表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-sql-trace-data-table)。

## <a name="test-results"></a>测试结果

“测试结果”一节包含负载测试中所有测试和方案的列表。 此节显示测试的名称、方案、运行的次数、失败的次数以及平均测试时间。 可选择某个测试的名称以打开“测试”表和查看该测试的更多详细信息  。 有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

> [!NOTE]
> 通过选择此节标题左侧的箭头，可以折叠和展开此节。

## <a name="page-results"></a>页结果

“页结果”一节包含负载测试中所有网页的列表。 此节显示 URL、方案、测试的名称、平均页面时间以及计数。 可选择某个页面的 URL 以打开“页”表和查看该页面的更多详细信息  。 有关详细信息，请参阅[如何：查看网页响应](../test/how-to-view-web-page-response-time-in-a-load-test.md)。

> [!NOTE]
> 通过选择此节标题左侧的箭头，可以折叠和展开此节。

## <a name="transaction-results"></a>事务结果

“事务结果”一节包含负载测试中所有事务的列表。 此节显示事务名称、方案、测试、响应时间、运行时间和计数。 可选择某个事务的名称以打开“事务”表，并查看该事务的更多详细信息  。 有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

> [!NOTE]
> 通过选择此节标题左侧的箭头，可以折叠和展开此节。

百分比值报告以下事务信息：

- 在 \< 秒之内完成了事务总数的 90%。

- 在 \< 秒之内完成了事务总数的 95%。

## <a name="system-under-test-resources"></a>受测系统的资源

“测试中系统的资源”一节包含一个计算机列表，这些计算机是为其生成负载的一组目标计算机。 除代理或控制器之外，这些计算机还包括您从中收集计数器集的任何计算机。 此节显示计算机名称、处理器时间百分比 (%) 和可用内存。 可以选择某个计算机名称以打开“测试中的系统”关系图，并查看不同时间的资源使用情况  。 有关详细信息，请参阅[在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)。

> [!NOTE]
> 通过选择此节标题左侧的箭头，可以折叠和展开此节。

## <a name="controller-and-agent-resources"></a>控制器和代理资源

“控制器和代理资源”一节包含用于运行测试的计算机列表。 此节显示计算机名称、处理器时间百分比 (%) 和可用内存。 可以选择某个计算机名称以打开“控制器和代理”关系图，并查看不同时间的资源使用情况  。 有关详细信息，请参阅[在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)。

> [!NOTE]
> 通过选择此节标题左侧的箭头，可以折叠和展开此节。

## <a name="errors"></a>错误

“错误”一节包含负载测试期间发生的所有错误的列表。 此节显示错误类型和子类型、计数以及最后一条消息。 可以选择某个错误以打开“错误”表，并查看该错误的更多详细信息  。 有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

> [!NOTE]
> 通过选择此节标题左侧的箭头，可以折叠和展开此节。

## <a name="print-a-summary"></a>打印摘要

通过选择负载测试摘要上的快捷菜单中的“打印”，可以打印该负载测试摘要  。 通过选择负载测试摘要上的快捷菜单中的“打印预览”，可以预览打印内容  。 还可以直接从预览屏幕上进行打印。

## <a name="see-also"></a>请参阅

- [分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)