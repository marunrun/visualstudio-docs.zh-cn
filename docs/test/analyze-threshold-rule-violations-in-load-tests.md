---
title: 分析负载测试中的阈值规则冲突
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.threshholdresult
helpviewer_keywords:
- load tests, thresholds
- threshold violations
- threshold counts
- load tests, threshold violations
- load test results, analyzing threshold violations
- thresholds in load tests
ms.assetid: 969ed346-cf2e-4d48-82b3-edb3e075e1c0
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7ffff5818c5d3c7085ef3bebcc29c31a363a09b9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665341"
---
# <a name="analyzing-threshold-rule-violations-in-load-tests-using-the-load-test-analyzer"></a>使用负载测试分析器分析负载测试中的阈值规则冲突

阈值规则与特定的性能计数器关联，存在冲突意味着性能计数器超过或低于设定的值。 运行负载测试时，可以依据之前设置的阈值规则分析所发生的冲突。

如果发生任何冲突，负载测试分析器的状态栏上将显示“阈值冲突”超链接，并指明发生的冲突数量   。 选择超链接将显示阈值冲突表。 还可以在“计数器”窗口和关系图上查看阈值冲突  。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="view-threshold-violations-in-the-table"></a>在表格中查看阈值冲突

阈值冲突表显示前 1,000 个冲突。 下面举例说明了一个表：

|列|说明|默认情况下可见|
|-|-|-|
|时间|负载测试过程中发生冲突的时间。|是|
|计算机|发生冲突的测试计算机的名称。 **注意：** 在远程测试机组 (Rig) 上运行负载测试时，这一项很重要。|是|
|类别|发生冲突的性能计数器的类别。|是|
|计数器|发生冲突的性能计数器的名称。|是|
|实例|发生冲突的性能计数器实例。|是|
|消息|描述阈值冲突的消息。 例如，值 5 超出了值 0 的临界阈值  。|是|

> [!NOTE]
> 选择列标题可以对表进行排序。

有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

## <a name="view-threshold-violations-in-the-counters-panel"></a>在计数器面板中查看阈值冲突

可以在“计数器”面板中列有负载测试的性能计数器的树中查看阈值冲突  。 “计数器”面板中的图标表示阈值冲突  。 该图标可以为如下所述的几种图标之一：

该图标可以为如下所述的几种图标之一：

![没有阈值冲突](../test/media/icon_ltest_1.gif) 无示阈值冲突。

![上次间隔中出现严重阈值冲突](../test/media/icon_ltest_2.gif) 在上一个间隔内发生严重阈值冲突。

![前一间隔中出现严重阈值冲突](../test/media/icon_ltest_3.gif) 在前面的某个间隔内发生严重阈值冲突。

![上次间隔中出现警告阈值冲突](../test/media/icon_ltest_4.gif) 在上一个间隔内发生警告阈值冲突。

![前一间隔中出现警告阈值冲突](../test/media/icon_ltest_5.gif) 在前面的某个间隔内发生警告阈值冲突。

也可以在关系图上显示阈值冲突。 阈值图标显示在关系图上发生阈值冲突的数据点旁边。

在计数器树中，阈值冲突的图标从特定计数器节点向上传播到根节点。 这会提醒您注意可能由于树未展开而在树中不可见的计数器上发生的冲突。

## <a name="view-threshold-violations-on-the-graph"></a>在关系图上查看阈值冲突

可以在关系图上查看阈值冲突。 与“计数器”面板类似，关系图上的图标也表示阈值冲突  。 图标显示在关系图上发生阈值冲突的数据点旁边。 如果阈值冲突发生在关系图中未显示的计数器上，则可以通过将该计数器从“计数器”面板拖到关系图上来将该计数器添加到关系图中  。

有关详细信息，请参阅[在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)。

## <a name="see-also"></a>请参阅

- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)