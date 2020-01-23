---
title: 分析负载测试结果和错误
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.pageresult
- vs.test.load.dialog.column
- vs.test.load.monitor.requestresult
- vs.test.load.monitor.testresult
- vs.test.load.monitor.table.view
- vs.test.load.monitor.agentresult
- vs.test.load.monitor.transactionresult
helpviewer_keywords:
- tables, Load Test Viewer options
- load test results, tables
- load tests, Load Test Viewer
- data [Visual Studio ALM], load test tables
- Load Test Viewer, tables
- load tests, results tables
ms.assetid: 0a84bda3-6051-45eb-9c7f-d57419e1f97d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c5e337c30a4b6a08f123ef7ee33dee704e9412de
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75565170"
---
# <a name="analyze-load-test-results-and-errors-in-the-tables-view-of-the-load-test-analyzer"></a>在负载测试分析器的表视图中分析负载测试结果和错误

查看负载测试运行的结果时，可以显示不同的窗格，从而以不同的方式分析数据。 你可以查看图形形式的数据，从而了解数据随时间的变化情况，也可以查看详细信息表形式的数据。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

要切换到表视图，请选择负载测试工具栏上的“表”   。 若要在不同的表之间切换，请使用表网格上方的工具栏上的“表”下拉列表  。 在表视图中，一次最多可以查看四个表。 有关详细信息，请参阅本主题中的[平铺负载测试表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#tile-load-test-tables)。

在整个负载测试运行期间，表中显示的大多数性能计数器数值都是累积的。 名为“最后一个”的列是个例外，它们表示最近的采样间隔内的值  。

> [!NOTE]
> 名为“最后一个”的列仅在执行负载测试时可用  。 负载测试完成后，这些列即变为不可用。

对于大多数表而言，都可以通过选择要作为排序依据的列标题来进行排序。 默认情况下，有些表并不显示所有可用的列。 如果有列可用，可向表中添加列。 若要添加列，请右键单击该表，然后选择“添加/删除列”  。

> [!NOTE]
> 可以将数据从表复制到 Excel 等其他应用程序中，供其他分析之用。

## <a name="the-load-test-tables"></a>负载测试表

下表列出了可用于分析负载测试运行的表。

|表名称|描述|
|-|-|
|错误|显示在负载测试运行期间发生的错误的列表。 有关详细信息，请参阅[分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)和本主题中的[“错误”表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-errors-table)。|
|Pages|显示在负载测试运行期间访问的页的列表。 此表中的某些数据仅在负载测试完成后才可用。 有关详细信息，请参阅[如何：查看网页响应](../test/how-to-view-web-page-response-time-in-a-load-test.md)。|
|请求|显示负载测试期间发出的各个请求的详细信息。 其中包括所有 HTTP 请求以及相关请求（如图像）。 有关详细信息，请参阅本主题中的[“请求”表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-requests-table)。|
|SQL 跟踪|显示 SQL 跟踪的结果。 此表仅在负载测试完成后、并且在测试期间使用了 SQL 跟踪的情况下才可用。 有关详细信息，请参阅本主题中的 [SQL 跟踪数据表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-sql-trace-data-table)。|
|计数|显示负载测试期间各个测试运行的详细信息。 有关详细信息，请参阅本主题中的[“测试”表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-tests-table)。|
|阈值|显示在负载测试运行期间发生的阈值规则冲突的列表。 有关详细信息，请参阅[分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)。|
|事务|显示负载测试运行期间发生的事务的列表。 有关详细信息，请参阅本主题中的[“事务”表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-transactions-table)。|
|代理|仅当负载测试使用测试控制器和测试代理时显示。 显示在负载测试运行期间使用的代理的列表。 “代理”表包含代理所测试的请求数以及这些请求中的失败请求数。 此外，“代理”表还包含代理所测试的负载测试测试组合中的测试数以及这些测试中的失败测试数。|
|测试详细信息|显示负载测试的测试组合中所包含的测试的详细信息。 这些详细信息包括测试名称、测试所在的方案、测试开始时间、运行测试所用的时间长短以及指示测试是否通过的测试结果。 如果测试未通过，则“详细信息”列中出现一个链接  。 你可以选择该链接以进入 Web 性能测试编辑器，其中突出显示了未通过的请求。|

## <a name="collect-percentile-data"></a>收集百分比数据

有些负载测试表可能包含一些附加列，其中包含基于网络模拟分成若干个组的百分点数据和响应时间。 默认情况下，不收集这些数据。 仅当你将结果保存到数据库而不是本地保存时，百分比数据才可用。 有关详细信息，请参阅[管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)。 此外，若要收集此数据，请在“负载测试编辑器”中的“运行设置”节点下，选择要更改的特定运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“StatisticsOnly”或“AllIndividualDetails”     。 有关详细信息，请参阅[如何：查看网页响应](../test/how-to-view-web-page-response-time-in-a-load-test.md)。

## <a name="the-requests-table"></a>请求表

“请求”表显示负载测试期间发出的各个请求的详细信息  。 其中包括所有 HTTP 请求以及相关请求（如图像）。 “请求”表按测试和方案列出请求，因为一个请求可以包含在许多测试和方案中。

下表列出了“请求”表中的列  ：

|列|描述|默认情况下可见|
|-|-|-|
|**请求**|请求的 URL。 例如，home.html 或 orange-arrow.gif   。|是|
|**方案**|方案的名称。|是|
|**测试**|测试的名称。|是|
|**总计**|负载测试运行期间发出的此 Web 性能测试请求的总数。 其中包括通过的请求和失败的请求，但不包括缓存的请求，因为它们不发送到 Web 服务器。|是|
|**通过**|请求发出并通过的次数。|否|
|**已失败**|请求发出但失败的次数。 此列中的项显示为超链接。 选择任一超链接可在“负载测试错误”对话框中查看各个错误的列表  。 有关详细信息，请参阅[分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)。|是|
|**已缓存**|请求已缓存的总次数。|否|
|**请求数/秒**|负载测试运行期间每秒的请求数。|否|
|**通过数/秒**|负载测试运行期间此请求的实例每秒通过的数目。|否|
|**失败数/秒**|负载测试运行期间此请求的实例每秒失败的数目。|否|
|**第一字节时间**|接收响应的第一个字节所用的平均时间，是从请求发送到 Web 服务器之时开始计算的。 单位为秒。|否|
|**响应时间**|接收请求的整个响应所用的平均时间，是从请求发送到 Web 服务器之时开始计算的。 单位为秒。|是|
|**内容长度**|请求的响应内容的平均长度。 单位为字节。|是|

## <a name="the-tests-table"></a>测试表

“测试”表显示负载测试期间各个测试运行的详细信息  。 该表按测试和方案列出测试，因为一个测试可以包含在许多方案中。

下表列出了“测试”表中的列  。

|列|描述|默认情况下可见|
|-|-|-|
|**测试**|测试的名称。|是|
|**方案**|方案的名称。|是|
|**总计**|该测试在方案中运行的总次数。 其中包括测试通过和失败的次数。|是|
|**通过**|该测试在方案中运行并通过的次数。|是|
|**已失败**|该测试在方案中运行但失败的次数。 此列中的项显示为超链接。 选择任一超链接可在“负载测试错误”对话框中查看各个错误的列表  。 有关详细信息，请参阅[分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)。|是|
|**测试数/秒**|负载测试运行期间每秒的测试数。|是|
|**通过数/秒**|负载测试运行期间此测试的实例每秒通过的数目。|否|
|**失败数/秒**|负载测试运行期间此测试的实例每秒失败的数目。|否|
|**测试时间**|负载测试运行期间执行测试所用的平均时间。 单位为秒。|是|
|**90% 测试时间**|测试时间值的 90%。|否|
|**95% 测试时间**|测试时间值的 95%。|是|
|**请求数/测试**|Web 性能测试中的平均请求数。|否|

## <a name="the-transactions-table"></a>事务表

“事务”表显示负载测试运行期间发生的事务的列表  。 这里的事务是指在 Web 性能测试中定义的事务，或者是指在单元测试中定义的计时器， 而不是指数据库事务。

下表列出了“事务”表中的列  。

> [!NOTE]
> 若要查看所有列，必须启用与活动的运行设置关联的“计时详细信息存储”属性。 有关详细信息，请参阅[如何：指定计时详细信息存储属性](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md)。

|列|描述|可见，但没有计时详细信息|
|-|-|-|
|**事务**|事务的名称。|是|
|**方案**|方案的名称。|是|
|**测试**|测试的名称。|是|
|**总计**|负载测试运行期间发出的事务的总数。|是|
|**事务时间**|负载测试运行期间执行事务所用的时间。 对于 Web 性能测试，思考时间也包括在内。 单位为秒。|否|
|**响应时间**|负载测试运行中 Web 性能测试事务的响应时间。 响应时间与事务时间的不同之处在于，响应时间不包括事务期间发生的任何思考时间。 单位为秒。|否|
|**平均事务时间**|平均事务时间。 此时间包括思考时间。 例如，如果你有三个请求并且每个请求都有一个思考时间，此时间将包括这些思考时间和执行请求的实际时间。|否|
|**平均响应时间**|负载测试运行中 Web 性能测试事务的平均响应时间。 响应时间与事务时间的不同之处在于，响应时间不包括事务期间发生的任何思考时间。 单位为秒。|否|
|**最小响应时间**|不包括思考时间。|否|
|**最大响应时间**|不包括思考时间。|否|
|**中值响应时间**|不包括思考时间。|否|
|**90% 响应时间**|事务时间值的 90%。 不包括思考时间。 **注意：** 这与使用“90% 事务时间”值的 Visual Studio 团队系统 2008 负载测试代理不同  。|否|
|**95% 响应时间**|事务时间值的 95%。 不包括思考时间。 **注意：** 这与使用“95% 事务时间”值的 Visual Studio 团队系统 2008 负载测试代理不同  。|否|
|**99% 响应时间**|事务时间值的 99%。 不包括思考时间。|否|
|**标准偏差响应时间**|不包括思考时间。|否|

## <a name="the-errors-table"></a>错误表

运行负载测试时，可以分析发生的错误。 分析错误和调整测试是负载测试过程的重要部分。 如果发生任何错误，将在负载测试状态栏上显示“错误”超链接，并指出发生的错误数  。 若要显示错误表，请选择该超链接。

错误表按错误的类型和子类型对负载测试过程中发生的错误进行分组。 该表中还有一个“总计”行，用来指出发生的所有错误的总数  。

错误表中包含以下列：

|列|描述|默认情况下可见|
|-|-|-|
|类型|错误类型。 例如，HttpError。|是|
|子类型|错误的子类型。 例如，LoadTestException。|是|
|计数|负载测试过程中发生的此类型的错误数。 此列中的项显示为超链接。 选择任意超链接可以查看各个错误的列表。|是|
|最后一条消息|描述错误的消息。 例如，404 - NotFound。|是|

有关详细信息，请参阅[使用负载测试表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

### <a name="drill-down-to-the-error-list"></a>深入了解错误列表

错误表按错误的类型和子类型对错误进行分组。 要查看包含各个错误的表，可以显示“负载测试错误”对话框  。 若要显示该对话框，请在“错误”表的“计数”列中选择超链接  。 还可以通过右键单击“错误”表中已填充的行，然后选择“错误”来显示该对话框  。

> [!NOTE]
> 系统仅收集任何错误类型和子类型组合的前 1,000 个实例。 显示“负载测试错误”对话框时，最多可以看到该错误的前 1,000 个实例  。

“负载测试错误”表包含以下列  ：

|列|描述|
|-|-|
|**时间**|负载测试过程中发生错误的时间。|
|**代理**|发生错误的代理计算机的名称。 使用测试控制器和测试代理运行负载测试时此设置很重要。 有关详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。|
|**测试**|发生错误的 Web 性能测试的名称。|
|**方案**|发生错误的方案的名称。|
|**请求**|发生错误的请求的 URL。|
|**Type**|错误类型。 例如，HttpError。|
|**子类型**|错误的子类型。 例如，LoadTestException。|
|**文本**|错误消息的文本。 例如，404 - NotFound。|
|**堆栈**|此列中的项为空，或者“堆栈”一词显示为超链接格式  。 选择此超链接可以查看错误的堆栈跟踪。|
|**详细信息**|此列中的项为空，或者“TestLog”一词显示为超链接格式  。 此链接可以帮助你隔离负载测试中的错误。 例如，选择 Web 性能测试请求错误上的“TestLog”链接会在 Web 性能测试结果查看器中打开 Web 性能测试的结果，并突出显示该请求错误  。|

> [!NOTE]
> 选择列标题可以对表进行排序。

## <a name="the-sql-trace-data-table"></a>SQL 跟踪数据表

可以在负载测试运行过程中收集 SQL 跟踪数据，以供日后分析。 通过收集跟踪数据，可以识别出在所测试的 SQL Server 数据库中运行速度最慢的查询和存储过程。

如果启用了 SQL 跟踪，在负载测试运行期间便会创建一个包含跟踪数据的文件。 在测试运行结束时，该数据会自动保存到负载测试结果存储区中，跟踪文件会被删除。 完成负载测试后，可在“SQL 跟踪”表中分析跟踪数据  。

### <a name="to-view-sql-trace-data"></a>查看 SQL 跟踪数据

1. 在负载测试分析器中，选择工具栏上的“表”以确保显示表网格  。

2. 从“表”下拉列表框中选择“SQL 跟踪”   。

3. 在测试运行过程中收集到的跟踪数据将显示在网格中。 表中将列出运行速度最慢的几个 SQL 操作，并按照持续时间来排序，最慢的放在最上面。 通常，“持续时间”列是第一个要检查的列  。 该数据以毫秒显示。

   将显示如下所示的列：

    - **event 类**

    - **持续时间**

    - **CPU**

    - **读取次数**

    - **写入次数**

    - **TextData**

    - **StartTime**

    - **EndTime**

   如果要跟踪 SQL 事件而不是跟踪在这些列中标识出的数据，则可以使用独立于 Visual Studio 的 SQL 事件探查器工具来设置自己的自定义 SQL 跟踪。

## <a name="tile-load-test-tables"></a>平铺负载测试表

查看负载测试运行的结果时，可以以详细表的形式查看数据。 要切换到表视图，请选择负载测试工具栏上的“表”   。 提供以下表：“错误”、“页面”、“请求”、“SQL 跟踪”、“测试”、“阈值”和“事务”        。 有关详细信息，请参阅[使用负载测试表](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

在表视图中，一次最多可查看四个表，而不会重叠。

### <a name="to-tile-tables"></a>对表进行平铺

1. 在负载测试分析器工具栏上，选择“表”   。

     此时将打开表视图。 默认的布局为两个水平的面板。

2. 在负载测试分析器工具栏上，选择布局按钮，然后选择下列选项之一   ：

    - 一个面板 

    - 两个水平的面板 

    - 三个水平的面板 

    - 四个水平的面板 

3. 若要在不同的表之间切换，请使用各个面板中表网格上方的下拉列表。

    > [!NOTE]
    > 不能在多个面板中显示同一个表。 如果将一个面板中显示的表更改为另一个面板中已经显示的表，则这些表将切换面板。

## <a name="see-also"></a>请参阅

- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)
- [在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)
- [分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [负载测试结果摘要概述](../test/load-test-results-summary-overview.md)
