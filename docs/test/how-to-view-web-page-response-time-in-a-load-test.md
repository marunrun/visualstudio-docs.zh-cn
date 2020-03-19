---
title: 负载测试中的页面响应时间
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, response times
- response times in load tests
- load test results, response times
ms.assetid: e61c49f3-3161-45b1-9220-08b5459065a2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cf8bc1205658899a51cf1a50e83a9a8b34034b25
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594313"
---
# <a name="how-to-view-web-page-response-time-in-a-load-test-using-the-load-test-analyzer"></a>如何：使用负载测试分析器在负载测试中查看网页响应时间

加载每个网页所需的时间称为“响应时间”  。 创建 Web 性能测试时，可以为 Web 性能测试中的每个网页请求设置响应时间目标。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

如果在负载测试中的压力下运行 Web 性能测试，你将能够分析各页的以下信息：

- 页面的平均响应时间。

- 满足页面的响应时间目标的测试迭代次数百分比。

- 可以使用负载测试分析器中的表视图或关系图视图来分析网页响应时间  ：

- 在表视图中分析网页响应时间

- 在关系图视图中分析网页响应时间

## <a name="view-response-time-data-in-a-table"></a>在表中查看响应时间数据

1. 在负载测试分析器中，选择工具栏上的“表”以确保显示表网格   。

2. 在“表”下拉列表框中，选择“页”   。

3. 网格中将显示每页的数据。 通常会显示以下列。

   |列标题|描述|
   |-|-|
   |**页**|网页的名称。|
   |**方案**|方案的名称。 如果在 Web 性能测试中有多个方案，则这一列很重要。|
   |**测试**|Web 性能测试的名称。 如果在负载测试中有多个 Web 性能测试，则这一列很重要。|
   |**Network**|网络类型。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**总计**|对该网页的请求的总数。 这是负载测试中所有迭代中的请求的总数。|
   |**平均值**|平均页面响应时间。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**最小值**|最短页面响应时间。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**中值**|中线页面响应时间。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**90%**|响应时间的 90%。 此数据指示 90% 的页面的响应时间比此数字低，10% 的页面的响应时间比此数字高。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**95%**|响应时间的 95%。 此数据指示 95% 的页面的响应时间比此数字低，5% 的页面的响应时间比此数字高。|
   |**99%**|响应时间的 99%。 此数据指示 99% 的页面的响应时间比此数字低，1% 的页面的响应时间比此数字高。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**最大值**|最长页面响应时间。<br /><br /> 默认情况下，不收集这些数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**标准偏差**|默认情况下，不收集标准偏差数据。 要收集这些数据，请在“负载测试编辑器”中的“运行测试”节点下，选择要更改的运行设置节点   。 在“属性”窗口中，为“计时详细信息存储”属性，选择“AllIndividualDetails”    。|
   |**页面时间**|对该网页的所有请求的平均响应时间。|
   |**目标**|页面时间目标。 这是页面的常数值。 **注意：** 仅当在 Web 性能测试中为请求定义了目标时才会显示“页面时间目标”。|
   |**符合目标百分比(%)**|对网页的请求中满足响应时间目标的请求的百分比。|

   有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

## <a name="view-response-time-data-in-a-graph"></a>在关系图中查看响应时间数据

您还可以在关系图中查看响应时间数据，以了解负载测试期间这些数据随时间的变化情况。 这对于负载模式随测试的运行而增加的情况（例如，当使用单步负载模式时）尤其有用。 有关详细信息，请参阅[编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)。

在关系图中查看响应时间数据：

1. 在负载测试分析器中，选择工具栏上的“关系图”以确保显示该关系图   。

2. 在“计数器”窗口中，展开感兴趣的方案的节点（例如 `Scenario1`）  。

3. 展开你感兴趣的 Web 性能测试的节点。

4. 展开“页”节点  。

5. 展开您感兴趣的页的节点。

6. 右键单击“符合目标的页面百分比”，然后选择“在关系图上显示计数器”   。

    数据即添加到关系图中。

7. （可选）对 Avg. Page Time、    Page Response、Time Goal 和 Total Pages 重复上一步骤。

   > [!NOTE]
   > Page Response Time Goal 是常数  。

   有关详细信息，请参阅[在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)。

## <a name="see-also"></a>请参阅

- [在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)
- [如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
