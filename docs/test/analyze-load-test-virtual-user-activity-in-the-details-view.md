---
title: 分析负载测试虚拟用户活动
ms.date: 10/03/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.activitychart
helpviewer_keywords:
- virtual user activity chart
- load test, virtual user activity chart
ms.assetid: 63f4bd42-3cfb-4eee-af68-e8334976539e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0289ff0d4a20eacc4f6801d9300d39df594bc79e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591228"
---
# <a name="analyzing-load-test-virtual-user-activity-in-the-details-view-of-the-load-test-analyzer"></a>在负载测试分析器的详细信息视图中分析负载测试虚拟用户活动

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**虚拟用户活动图**

![虚拟用户活动图](../test/media/virtual_actchart.png)

详细信息视图显示了虚拟用户活动图，该图用于直观地分析各虚拟用户在负载测试期间执行的操作   。 借助虚拟用户活动图，可查看用户活动的模式、负载模式，关联失败的测试或速度缓慢的测试，还可查看具有其他虚拟用户活动的请求  。 虚拟用户活动图还有助于确定 CPU 使用率峰值、每秒请求数谷值以及在这些峰值和谷值期间运行的测试或页面  。

> [!NOTE]
> 在运行要对其使用虚拟用户活动详细信息图的负载测试之前，必须使用负载性能测试编辑器来验证“计时详细信息存储”属性是否已设置为“AllIndividualDetails”选项    。

**详细信息图例面板**

![详细信息图例面板](../test/media/ltest_detailslegend.png)

详细信息图例面板显示在虚拟用户活动图中  。 使用详细信息图例窗格，可以基于多种不同条件来筛选测试、页和事务。 例如，可以从视图中移除某些测试或移除所有成功的测试，或者移除因某些故障而失败的测试。 还可以移除没有日志的所有测试。

可以突出显示失败的测试，以红色显示所有失败的测试。 还可以突出显示具有测试日志的测试。 具有日志的测试将显示为绿色。

**筛选结果面板**

![筛选结果面板](../test/media/ltest_filterresults.png)

筛选结果面板显示在虚拟用户活动图中  。 筛选结果面板可以按以下方式进行筛选：

- “仅显示含日志的结果”仅显示具有关联测试日志的测试结果。 

- “显示成功结果”显示成功的结果。 

- “显示包含错误的结果”显示包含可以帮助调试的错误的结果。 

## <a name="tasks"></a>任务

|任务|关联主题|
|-|-|
|**运行负载测试：** 创建负载测试并将其配置为启用虚拟用户活动数据收集后，必须运行该测试，直到全部完成后才能查看其“虚拟用户活动图”  。||
|**查看包含虚拟用户活动数据的负载测试结果：** 创建、配置并运行完负载测试后，可以使用虚拟用户活动图查看“虚拟用户活动图”  。|-   [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)<br />-   [如何：分析虚拟用户在负载测试期间的操作](../test/how-to-analyze-virtual-user-activity-during-a-load-test.md)|
|**隔离负载测试中的性能问题：** 可以使用“虚拟用户活动图”来帮助隔离负载测试中的性能问题  。|-   [演练：使用虚拟用户活动图隔离问题](../test/walkthrough-use-the-virtual-user-activity-chart-to-isolate-issues.md)|

## <a name="see-also"></a>请参阅

- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)
