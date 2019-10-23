---
title: 适用于负载测试运行设置的计时详细信息存储属性
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, properties
- load tests, run settings
ms.assetid: 867a9c21-0909-4963-bc02-d41e9393008c
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4b8ef3edb592b003a8c42ef954129c3bafd3ffc8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653346"
---
# <a name="how-to-specify-the-timing-details-storage-property-for-a-load-test-run-setting"></a>如何：为负载测试运行设置指定计时详细信息存储属性

在用“新建负载测试向导”创建负载测试之后，可使用“负载测试编辑器”来更改设置以满足测试需求和目标   。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

可以在“属性”窗口中编辑运行设置的“计时详细信息存储”属性值   。 “计时详细信息存储”属性可设置为以下任一选项  ：

- **所有的详细信息：** 收集并存储测试过程中发出的每个测试、事务和页面的单独计时数据。

  > [!NOTE]
  > 必须选择“所有的详细信息”选项才能启用负载测试结果中的虚拟用户数据信息  。 有关详细信息，请参阅[在“详细信息”视图中分析虚拟用户活动](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)。

- **无：** 不收集任何计时详细信息。 但是，平均值仍然可用。

- **仅统计信息：** 存储单独的计时数据，但仅作为百分比数据。 此选项节省空间资源。

  **“计时详细信息存储”属性注意事项**

  如果启用了“计时详细信息存储”属性，则在负载测试过程中执行各个测试、事务和页所需的时间都将存储在负载测试结果存储库中  。 由此，90% 和 95% 的数据显示在负载测试分析器的“测试”、“事务”和“页”表中     。

  如果启用了“计时详细信息存储”属性，则通过将该属性的值设置为“StatisticsOnly”或“AllIndividualDetails”，可对所各测试、页和事务进行计时，并根据各个计时数据计算百分比数据    。 它们的区别是，使用“StatisticsOnly”选项时，在计算完百分比数据之后，将从储存库中删除单个计时数据  。 删除数据可以减少使用计时详细信息时储存库中所需的空间量。 不过，可能需要使用 SQL 工具以其他方式来处理计时详细信息数据，在这种情况下，应使用“AllIndividualDetails”选项，以便可以使用计时详细信息数据进行该处理  。 此外，如果将属性设置为“AllIndividualDetails”，则可以在负载测试运行结束后，使用负载测试分析器中的“虚拟用户活动”图来分析虚拟用户活动    。 有关详细信息，请参阅[在“详细信息”视图中分析虚拟用户活动](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)。

  负载测试结果储存库中存储计时详细信息数据所需的空间量可能会非常大，尤其是对于运行时间较长的负载测试。 此外，在负载测试结束时将此数据存储到负载测试结果储存库中所需的时间也较长，因为在负载测试执行完成之前，此数据一直存储在负载测试代理上。 默认情况下，将启用“计时详细信息存储”属性  。 如果这对测试环境来说有问题，则可能需要将“计时详细信息存储”设置为“无”   。

  计时详细信息数据在运行期间存储在 LoadTestItemResults.dat 文件中，并在负载测试完成后发送回控制器  。 如果负载测试的运行持续时间很长，则该文件会很大。 如果代理计算机上没有足够的磁盘空间，这将成为问题。

  如果要从早期版本的 Visual Studio 负载测试升级项目，请使用下面的过程来启用完整详细信息收集。

## <a name="to-configure-the-timing-details-storage-property-in-a-load-test"></a>配置负载测试中的计时详细信息存储属性

1. 在负载测试编辑器中打开一个负载测试。

2. 展开负载测试中的“运行设置”节点  。

3. 选择要配置的运行设置，例如“Run Settings1[Active]”  。

4. 打开“属性”窗口  。 在“视图”菜单上选择“属性窗口”   。

5. 在“结果”类别下，选择“计时详细信息存储”属性，然后选择“所有的详细信息”    。

     为“计时详细信息存储”属性配置“所有的详细信息”设置之后，可以运行负载测试并查看“虚拟用户活动图”    。 有关详细信息，请参阅[如何：分析虚拟用户在负载测试期间的操作](../test/how-to-analyze-virtual-user-activity-during-a-load-test.md)。

## <a name="see-also"></a>请参阅

- [在详细信息视图中分析虚拟用户活动](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)
- [演练：使用虚拟用户活动图隔离问题](../test/walkthrough-use-the-virtual-user-activity-chart-to-isolate-issues.md)