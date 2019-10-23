---
title: 在负载测试结果中的关系图上添加和删除计数器
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load test results graphs, adding counters
- load test results graph
- load test, results graph
- load test results, graphs
ms.assetid: 81536233-1962-40d9-9511-0b4633814d90
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b589e45fe32aff1ce0eea338675d42c3e3ea944a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72644364"
---
# <a name="how-to-add-and-delete-counters-on-graphs-in-load-test-results"></a>如何：在负载测试结果中的关系图上添加和删除计数器

可以使用“计数器”  面板向关系图添加性能计数器。

![已向关系图中添加计数器](../test/media/ltest_selectcounter.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**性能计数器采样间隔注意事项**

基于负载测试的长度，在负载测试运行设置中为“采样率”属性选择一个值。  较小的采样速率（如 5 秒默认值）需要占用负载测试结果数据库中的更多空间。 对于更长的负载测试，增加采样速率会减少收集的数据量。 有关详细信息，请参阅[如何：指定采样率](../test/how-to-specify-the-sample-rate-for-a-load-test.md)。

下面是有关采样速率的一些准则：

|负载测试持续时间|建议的采样速率|
|-|-----------------------------|
|\< 1 小时|5 秒|
|1 - 8 小时|15 秒|
|8 - 24 小时|30 秒|
|> 24 小时|60 秒|

**包括计时详细信息以收集百分比数据的注意事项**

负载测试编辑器的运行设置中有一个名为“计时详细信息存储”的属性  。 如果启用了“计时详细信息存储”属性，则在负载测试过程中执行各个测试、事务和页所需的时间都将存储在负载测试结果存储库中  。 这使得 90% 和 95% 的数据显示在“负载测试分析器”  的“测试”、“事务”和“页”表中。

可通过两种方法来启用运行设置属性中的“计时详细信息存储”属性：“StatisticsOnly”和“AllIndividualDetails”    。 无论采用哪个选项，所有单个测试、页和事务均会计时，且根据单个计时数据来计算百分比数据。 它们的区别是，使用“StatisticsOnly”选项时，在计算完百分比数据之后，将立即从存储库中删除单个计时数据  。 删除数据可以减少使用计时详细信息时储存库中所需的空间量。 但是，高级用户可能需要使用 SQL 工具以其他方式来处理计时详细信息数据。 如果是这样，则应使用“AllIndividualDetails”选项，以便计时详细信息数据可用于该处理。  此外，如果将属性设置为“AllIndividualDetails”  ，则可以在负载测试运行结束后，使用“负载测试分析器”  中的“虚拟用户活动”  图来分析虚拟用户活动。 有关详细信息，请参阅[在“详细信息”视图中分析虚拟用户活动](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)。

负载测试结果储存库中存储计时详细信息数据所需的空间可能会非常大，尤其是对于运行时间较长的负载测试。 另外，在负载测试结束时将此数据存储到负载测试结果储存库中所需的时间也较长，因为在负载测试完成执行之前此数据一直存储在负载测试代理上。 负载测试完成时，数据将存储到储存库中。 默认情况下，将启用“计时详细信息存储”属性  。 如果这对测试环境来说有问题，则可能需要将“计时详细信息存储”设置为“无”   。

有关详细信息，请参阅[如何：指定计时详细信息存储属性](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md)。

## <a name="to-display-a-particular-performance-counter-on-a-load-test-graph"></a>在负载测试关系图上显示特定性能计数器

1. 在完成负载测试后或加载测试结果后，在负载测试分析器的工具栏中选择“关系图”  。

     “计数器”面板显示在关系图视图中  。

    > [!NOTE]
    > 如果看不到“计数器”  面板，请选择工具栏上的“显示计数器面板”  。

2. 在“计数器”  面板中，展开层次结构中的节点，直到找到希望以图形方式显示的性能计数器。

     例如，若要显示运行测试的计算机上的可用内存，请展开“计算机”，展开该计算机的节点，然后展开“内存”   。 将看到“Available MBytes”计数器  。

3. 选择要在上面显示性能计数器的关系图。

4. 在“计数器”面板中右键单击性能计数器，然后选择“在关系图上显示计数器”   。

    > [!TIP]
    > 若要暂时停止在关系图上显示性能计数器数据，请清除图例中性能计数器的复选框。 这样仍可以分析最小值、最大值和平均值统计信息，而不用在关系图上查看趋势线。 如果在分析问题时关系图包含几个重叠的性能计数器图形，这会非常有用。 有关详细信息，请参阅[使用关系图视图图例分析负载测试](../test/use-the-graphs-view-legend-to-analyze-load-tests.md)。

5. 若要从关系图删除性能计数器数据，请右击图例的“计数器”列中的性能计数器，然后选择“删除”   。

     \- 或 -

     右击关系图中的数据行并选择“删除”  。

     \- 或 -

     选择图例的“计数器”列中的性能计数器或关系图中的数据行，然后按 Delete   。

    > [!NOTE]
    > 也可以使用“在图例上添加计数器”命令选择将性能计数器放置在图例上而不是放置在关系图上  。

## <a name="see-also"></a>请参阅

- [在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)
- [如何：创建自定义图形](../test/how-to-create-custom-graphs-in-load-test-results.md)