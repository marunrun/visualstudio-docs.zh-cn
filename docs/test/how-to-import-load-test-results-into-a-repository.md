---
title: 如何：将负载测试结果导入存储库中
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- results, load test
- load test results, importing
- Load Test Results Repository
- load tests, importing results
ms.assetid: a955b3d2-c8ad-40dd-8ea3-9f1a271e1eed
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 16f6558373c111dbaf933184cf5ae23d00962b7a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949959"
---
# <a name="how-to-import-load-test-results-into-a-repository"></a>如何：将负载测试结果导入存储库中

运行负载测试时，在运行期间收集的信息都存储到负载测试结果储存库中。 负载测试结果储存库中包含性能计数器数据和有关任何错误的信息。 有关详细信息，请参阅[管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)。

可以使用“打开和管理负载测试结果”对话框，从“负载测试编辑器”中管理负载测试结果。 您可以打开、导入、导出和移除负载测试结果。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-import-results-into-a-repository"></a>将结果导入储存库

1. 从 Web 性能和负载测试项目中，打开负载测试。

2. 在嵌入式工具栏上，选择“打开和管理结果”。

     随即出现“打开和管理负载测试结果”对话框。

3. 在“请输入要用来查找负载测试结果的控制器名称”中选择一个控制器。 选择“\<本地>”以访问本地存储的结果。

     如果存在负载测试结果，它们将出现在“负载测试结果”列表中。 其中包括“时间”、“持续时间”、“用户”、“结果”、“测试”和“说明”列。 “测试”列包含测试的名称，“说明”列包含运行测试之前添加的可选说明。

4. 选择“导入”。

     随即出现“导入负载测试结果”对话框。

5. 在“文件名”框中，键入已存档的测试结果文件的名称，然后选择“打开”。

     \- 或 -

     浏览到该文件，然后选择“打开”。

    > [!NOTE]
    > 你在此步骤中指定的已存档测试结果文件必须已经通过执行“导出”操作创建完毕。

     随即会导入结果并将它们显示在“负载测试结果”列表中。

## <a name="see-also"></a>请参阅

- [管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [如何：从存储库导出负载测试结果](../test/how-to-export-load-test-results-from-a-repository.md)