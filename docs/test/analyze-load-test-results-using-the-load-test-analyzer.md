---
title: 分析负载测试结果
ms.date: 10/20/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, test results
- load tests, analyzing test results
- load tests, managing test results
ms.assetid: 8a4ba300-425d-447c-91d9-c53f4345feee
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9300dd1ebeaee9d87d2527dbc49fa66e319970c1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591224"
---
# <a name="analyze-load-test-results-using-the-load-test-analyzer"></a>使用负载测试分析器分析负载测试结果

使用负载测试分析器时，可在应用中查找性能瓶颈、识别错误并衡量所作的改进  。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

可通过以下方式分析负载测试结果：

- 监视正在运行的负载测试。

- 分析完成后的负载测试。

- 查看以前的负载测试的结果。

还可以创建报告，通过对比其中的两个或多个报告进行趋势分析，从而与利益干系人共享。 请参阅[报告负载测试结果以进行测试比较或趋势分析](../test/compare-load-test-results.md)。

不论是从 Visual Studio Enterprise 还是从命令行运行负载测试，也不论是在一台计算机上还是在远程计算机上运行负载测试，都可以完成这些任务。

## <a name="differences-between-analyzing-a-running-and-a-completed-load-test"></a>分析正在运行的负载测试与已完成的负载测试之间的区别

运行负载测试时，负载测试分析器显示在一个单独的选项卡上，其中显示有负载测试的名称和该测试的启动时间（例如，“LoadTest1 [12:40 PM]”）   。 在负载测试运行时，内存中会维护一个较小的性能计数器数据集。 你可以在负载测试运行时监视此数据集。 负载测试完成之后，你可以从数据库中分析完整的数据集。 在负载测试运行时所显示的数据与在负载测试完成后所显示的数据之间存在着差异。 例如，在负载测试完成之后才计算 90% 和 95% 响应时间数据。 在可用于分析数据的工具的功能方面也有一些差异。

运行负载测试时，有两个视图可用：“图”视图和“表”视图   。 通过关系图视图，可以绘制所收集的性能计数器  。 表视图提供所收集的每个测试、页、事务和请求的相关信息  。 您还可以获取一个列出错误的表。

默认情况下，当负载测试运行完成时，将显示摘要视图  。 可以使用工具栏在摘要视图、关系图视图、表视图和详细信息视图之间切换     。 可运用常用的 Visual Studio 窗口操作技巧停靠负载测试分析器或将其设置为浮动  。 分析已完成的负载测试运行时，可以同时打开多个负载测试分析器，以比较不同的负载测试运行  。

## <a name="tasks"></a>任务

|任务|关联主题|
|-|-|
|**访问负载测试的结果：** 在从“负载测试编辑器”运行负载测试时，负载测试结果会自动打开，并且正在运行的负载测试将显示在“负载测试分析器”  中。|-   [如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)|
|**向负载测试添加分析注释：** 执行分析时，可以向负载测试添加注释。 这些注释将随负载测试结果一起永久保存。 输入的说明也显示在与负载测试编辑器中“打开和管理测试结果”对话框中的负载测试关联的“说明”列中   。<br /><br /> 有关详细信息，请参阅[如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)。<br /><br /> 此外，在为负载测试结果创建 Excel 报表时也会显示注释。<br /><br /> 有关详细信息，请参阅[报告负载测试结果以比较测试或进行趋势分析](../test/compare-load-test-results.md)。||
|**分析负载测试的结果：** 访问负载测试运行数据之后，才能分析结果数据。 可以通过查看“负载测试摘要”来快速了解结果。 负载测试摘要以简洁、易读的格式显示关键结果。<br /><br /> 可以打印负载测试摘要， 以便于在向利益干系人传达结果时使用。<br /><br /> 您可以使用结果中的关系图和表来分析负载测试结果的详细信息。 其中包括“错误”、“页面”、“请求”、“SQL 跟踪”、“测试”、“阈值”和“事务”        。|-   [负载测试结果摘要概述](../test/load-test-results-summary-overview.md)<br />-   [如何：查看网页响应](../test/how-to-view-web-page-response-time-in-a-load-test.md)<br />-   [分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)<br />-   [在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)<br />-   [在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)|
|**分析负载测试结果中的虚拟用户活动，帮助隔离性能问题：** 可使用虚拟用户活动图来直观显示虚拟用户在负载测试期间正在执行的操作。 这可以帮助你隔离 CPU 峰值或每秒请求数谷值，并确定在这些峰值和谷值期间运行的是哪些测试或页面。|-   [在详细信息视图中分析虚拟用户活动](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)|
