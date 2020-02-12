---
title: 使用虚拟用户活动图表进行负载测试
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, virtual user activity chart
- virtual user activity chart, isolating performance issues
ms.assetid: d1c10fb9-cfeb-4e7f-9991-2d1e1103699e
author: jillre
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a437da5d95b758b908f1f1d4f7b76c50b6488a3c
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091842"
---
# <a name="walkthrough-using-the-virtual-user-activity-chart-to-isolate-issues"></a>演练：使用虚拟用户活动图隔离问题

在本演练中，你将了解如何使用虚拟用户活动图来隔离运行负载测试的各个虚拟用户所遇到的错误。

虚拟用户活动图用于可视化与负载测试关联的虚拟用户活动。 图中的每一行代表一个虚拟用户。 虚拟用户活动图显示每个虚拟用户在测试期间所执行的操作。 这样，你便可以通过查看用户活动的模式和负载模式来隔离性能问题，关联失败的或速度缓慢的测试，并且查看具有其他虚拟用户活动的请求。 只有在运行完负载之后，虚拟用户活动图才可用。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="prerequisites"></a>先决条件

- Visual Studio Enterprise

- 完成以下过程：

  - [记录和运行 Web 性能测试](/azure/devops/test/load-test/run-performance-tests-app-before-release#recordtests)。

  - [创建和运行负载测试](/azure/devops/test/load-test/run-performance-tests-app-before-release#create-a-load-test)

## <a name="open-the-colorwebapp-solution-created-in-the-previous-walkthroughs"></a>打开在前面演练中创建的 ColorWebApp 解决方案

1. 打开 Visual Studio。

2. 打开包含 LoadTest1.loadtest 的 ColorWebApp 解决方案   。 此负载测试结果是通过执行本主题开头先决条件部分列出的三个演练中的步骤得到的。

     本演练中的剩余步骤假定有一个名为 ColorWebApp 的 Web 应用程序、一个名为 ColorWebAppTest.webtest 的 Web 性能测试和一个名为 LoadTest1.loadtest 的负载测试   。

## <a name="run-the-load-test"></a>运行负载测试

运行负载测试以收集虚拟用户活动数据。

- 在负载测试编辑器中，选择工具栏上的“运行”按钮   。 LoadTest1 开始运行。

## <a name="isolate-issues-in-the-virtual-user-activity-chart"></a>在虚拟用户活动图中隔离问题

运行负载测试并收集虚拟用户活动数据之后，可以在虚拟用户活动图中使用负载测试分析器的“详细信息”视图查看负载测试结果中的数据   。 此外，还可以使用“虚拟用户活动图”来帮助隔离负载测试中的性能问题  。

### <a name="to-use-the-virtual-user-activity-chart-in-your-load-test-results"></a>在负载测试结果中使用虚拟用户活动图

1. 运行完负载测试之后，负载测试分析器中会显示负载测试结果的“摘要”页   。 选择工具栏上的“关系图”按钮  。

     此时将显示关系图视图。

2. 在“页响应时间”关系图上，右键单击其中一个阈值冲突图标附近，然后选择“转到用户详细信息”   。

    > [!NOTE]
    > 也可以使用负载测试编辑器工具栏中的“详细信息”按钮打开用户活动图   。 但如果使用“转到用户详细信息”选项，“虚拟用户活动图”将在关系图中右键单击的测试部分自动放大   。

     将显示详细信息视图，“虚拟用户活动图”的焦点在发生阈值冲突的时间段上  。

     在 y 轴上，水平绘图表示各个虚拟用户。 x 轴显示负载测试运行的时间线。

3. 在“虚拟用户活动图”下的“缩放到时间段”工具中，调整左侧和右侧的滑动条，直到两者都接近阈值冲突图标   。 这会更改“虚拟用户活动图”中的时间刻度 

4. 在“详细信息图例”中，选中“(突出显示错误)”对应的复选框   。 你会注意到，将突出显示引起阈值冲突的虚拟用户。

5. 在“筛选结果”面板中，清除“显示成功结果”和“HttpError”复选框，但保留选中“ValidationRuleError”复选框     。

     根据前面演练中配置的阈值冲突的指定，“虚拟用户活动图”只显示 Red.aspx 页中花费时间超过 3 秒的虚拟用户   。

6. 将鼠标光标停留在表示虚拟用户的水平线上，这些虚拟用户出现了阈值冲突的验证规则错误。

7. 将显示包含以下信息的工具提示：

    - **用户 ID**

    - **方案**

    - **测试**

    - **结果**

    - **Network**

    - **开始时间**

    - **持续时间**

    - **代理**

    - **测试日志**

8. 请注意，“测试日志”是一个链接  。 选择“测试日志”链接  。

9. 与日志关联的 ColorWebTest Web 性能测试将在“Web 性能测试结果查看器”中打开  。 这样便可隔离发生阈值冲突的位置。

     可使用“详细信息图例”和“筛选结果”面板中的各种设置来帮助隔离性能问题和负载测试中的错误   。 使用这些设置和“缩放到时间段”工具，可查看虚拟用户数据在“虚拟用户活动图”中的显示方式   。

## <a name="see-also"></a>请参阅

- [在详细信息视图中分析虚拟用户活动](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)
- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)
- [如何：为分发的负载测试创建测试设置](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)
- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)
- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)
