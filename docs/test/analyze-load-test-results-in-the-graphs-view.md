---
title: 在负载测试分析器的关系图视图中分析负载测试结果
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.graph.view
helpviewer_keywords:
- graphs, analyzing load tests
- load tests, graphs in Load Test Viewer
- Load Test Viewer, graphs
- load tests, results graphs
- load tests, using graphs
- load test results, graphs
ms.assetid: 4a919cd8-541c-40ee-be3b-352fabc56140
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dac639b8513e8ef675c6246476791b9351241130
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75591263"
---
# <a name="analyze-load-test-results-in-the-graphs-view-of-the-load-test-analyzer"></a>在负载测试分析器的关系图视图中分析负载测试结果

负载测试的结果以数据的形式显示在多个不同窗格中。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

要以关系图的形式显示测试结果，请选择负载测试工具栏上的“关系图”   。 每个单独的关系图将显示在一个面板中，关系图的名称显示在下拉列表的顶部。 若要在面板中显示不同的关系图，请从列表中选择不同的关系图名称。

一次最多可显示四个关系图面板。 通过使用面板布局工具栏按钮，可以在不同的面板布局之间进行切换  。

系统提供了一些内置的关系图。 你既可以按原样使用这些内置关系图，也可以对它们进行自定义。 此外，还可以创建自己的关系图。 有关详细信息，请参阅[如何：在关系图上添加和删除计数器](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)和[如何：创建自定义关系图](../test/how-to-create-custom-graphs-in-load-test-results.md)。

## <a name="built-in-graphs"></a>内置关系图

下表列出了可用于分析负载测试结果的内置关系图。

|关系图名称|说明|
|-|-|
|关键指示器|用于描述测试性能的基本情况（如用户负载、吞吐量和响应时间）的计数器。|
|测试响应时间|有关运行测试所用时间的数据。|
|页响应时间|负载测试期间访问的网页的平均响应时间。|
|测试中的系统|有关运行所测试的应用程序的计算机的信息。 其中包括有关内存使用、处理器、物理磁盘和进程的数据。<br /><br /> 默认情况下，只收集“Available Mbytes”（可用的兆字节数）和“Processor Time”（处理器时间）计数器。|
|控制器和代理|有关运行负载测试的计算机的信息。 其中包括有关内存使用、处理器、物理磁盘和进程的数据。<br /><br /> 默认情况下，只收集“Available Mbytes”（可用的兆字节数）和“Processor Time”（处理器时间）计数器。|
|事务响应时间|负载测试期间发生的事务的平均响应时间。|

可以在运行时和运行了测试之后在关系图上显示不同的计数器。

> [!NOTE]
> 只有响应时间性能计数器可以添加到自动生成的响应时间关系图中。

计数器信息同时显示在关系图中和关系图下方的图例中。 也可以放大关系图的某一部分。 有关详细信息，请参阅[如何：放大关系图的区域](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)。

## <a name="counters-displayed-in-graphs"></a>关系图中显示的计数器

关系图中会显示一些计数器  。 计数器引用在负载测试期间收集的数据，如每秒的测试数或平均测试时间。 有关计数器的详细信息，请参阅[为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)。

显示在关系图中的计数器的图例显示了几列有关负载测试运行的有用数据。 若要关闭关系图中任何数据的显示，请清除图例中对应行的复选框。

图例包含以下列：

|计数器|计数器的名称|
|-|-|
|实例|计数器实例的名称。|
|类别|计数器类别的名称。|
|Computer|计数器收集的计算机的名称。|
|颜色|关系图中的线的颜色。|
|范围|指示该计数器的关系图上 100 表示的数。 例如，对于其范围上限值为 10,000 的区域，关系图顶部的 100 标签表示 10,000。|
|最小值|指示计数器的最小值（以毫秒为单位）。|
|最大值|指示计数器的最大值（以毫秒为单位）。|
|平均值|指示计数器的平均值（以毫秒为单位）。|
|上一个|显示最近的采样间隔内的计数器的值（以毫秒为单位）。|

## <a name="tasks"></a>任务

|任务|关联主题|
|-|-|
|**使用图例自定义关系图**：关系图视图图例显示了与关系图关联的每个性能计数器的信息。 可以使用图例来移除性能计数器，在关系图中突出显示性能计数器，并自定义绘图选项。|-   [使用关系图视图图例分析负载测试](../test/use-the-graphs-view-legend-to-analyze-load-tests.md)|
|**在关系图上显示计数器**：通过将计数器放置在关系图上，可以将不同种类的数据添加到负载测试结果关系图中。|-   [如何：在图上添加和删除计数器](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)|
|**放大关系图**：完成负载测试后，可使用缩放条来放大并滚动到关系图的某一区域。 通过放大，可以更细致地检查在负载测试运行过程中所生成的数据。|-   [如何：放大关系图的区域](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)|
|**平铺关系图**：可以采用多个模式中的任意一个排列负载测试结果关系图。 最多可以平铺四个关系图。||
|**创建自定义关系图**：可以设计用于显示有关负载测试结果的特定信息的关系图。 可以通过指定关系图将显示的负载测试计数器来设计自定义关系图。|-   [如何：创建自定义关系图](../test/how-to-create-custom-graphs-in-load-test-results.md)|
|在关系图中导出性能计数器数据：位于关系图视图中时，可使用负载测试分析器工具栏上的“将关系图数据导出到 Excel”按钮将关系图数据导出到 Microsoft Excel     。||

## <a name="related-tasks"></a>相关任务

[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)

[如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)

[分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)

## <a name="see-also"></a>另请参阅

- [如何：在关系图上添加和删除计数器](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)
- [如何：创建自定义关系图](../test/how-to-create-custom-graphs-in-load-test-results.md)
- [如何：放大关系图的区域](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)
