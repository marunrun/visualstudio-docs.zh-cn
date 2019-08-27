---
title: 分析负载测试结果
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- results, load test
- load test results, accessing
- Load Test Viewer
- load tests, accessing
- load tests, analyzing
- load tests, results
- Load Test Viewer, viewing
ms.assetid: b0a3e694-2894-479b-b270-7e61e9fafacd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e4b14be6df351a6975fb8a7cf6fa506a5d4f6041
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979427"
---
# <a name="how-to-access-load-test-results-for-analysis"></a>如何：访问负载测试结果进行分析

在从“负载测试编辑器”运行负载测试时，负载测试结果会自动打开，并且正在运行的负载测试将显示在“负载测试分析器”中。 当您从命令行运行负载测试时，您必须手动访问负载测试结果。

已完成负载测试的负载测试结果包含从受测计算机定期收集到的性能计数器样本和错误信息。 可以在负载测试运行过程中收集大量性能计数器样本。 收集到的性能数据量取决于测试运行的长度、采样间隔、受测计算机的数量、要收集的计数器的数量、配置的数据收集器以及日志记录级别。 对于大型负载测试，所收集的性能数据量很容易达到数千兆字节。 有关详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-access-a-load-test-result"></a>访问负载测试结果

1. 从 Web 性能和负载测试项目中，打开负载测试。

2. 在负载测试编辑器的工具栏中，选择“打开和管理结果”按钮。

     显示“打开和管理结果”对话框。

3. 在“请输入要用来查找负载测试结果的控制器名称”中选择一个控制器。 选择“\<本地> - 无控制器”以访问本地存储的结果。

4. 在“显示以下负载测试的结果”中，选择要查看其结果的负载测试。 选择“\<显示所有测试的结果>”以查看所有测试的所有结果。

     如果存在负载测试结果，它们将出现在“负载测试结果”列表中。 其中包括“时间”、“持续时间”、“用户”、“结果”、“测试”和“说明”列。 “测试”列包含测试的名称，“说明”列包含运行测试之前添加的可选说明。

    > [!NOTE]
    > 显示结果时，最新的结果将在列表的顶部显示。

5. 在“负载测试结果”列表中，选择要分析的负载测试结果并选择“打开”。

6. 将显示“负载测试分析器”。 所选的负载测试结果显示在“摘要”视图中。 有关详细信息，请参阅[负载测试结果摘要概述](../test/load-test-results-summary-overview.md)。

     可以在“打开和管理结果”对话框中管理负载测试结果的其他方面，包括导入、导出和删除负载测试结果。 有关详细信息，请参阅[管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)。

## <a name="see-also"></a>请参阅

- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)