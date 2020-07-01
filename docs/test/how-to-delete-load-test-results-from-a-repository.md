---
title: 如何：从存储库删除负载测试结果
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- results, load test
- load tests, deleting results
- load test results, removing
- Load Test Results Repository
- load tests, removing results
- load test results, deleting
ms.assetid: c2afe36b-d061-4f0e-9580-c18569ec08f9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dd196076fb769f80c36ab8630eebf1e8a0f8b234
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287774"
---
# <a name="how-to-delete-load-test-results-from-a-repository"></a>如何：从存储库删除负载测试结果

运行负载测试时，在运行期间收集的信息都存储到负载测试结果储存库中。 负载测试结果储存库中包含性能计数器数据和有关任何错误的信息。 有关详细信息，请参阅[管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)。

可以使用“打开和管理负载测试结果”对话框，从“负载测试编辑器”中管理负载测试结果。 您可以打开、导入、导出和移除负载测试结果。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-delete-results-from-a-repository"></a>从储存库中删除结果

1. 从 Web 性能和负载测试项目中，打开负载测试。

2. 在嵌入式工具栏上，选择“打开和管理结果”。

     随即出现“打开和管理负载测试结果”对话框。

3. 在“请输入要用来查找负载测试结果的控制器名称”中选择一个控制器。 选择“\<Local - No controller>”，以访问本地存储的结果。

4. 在“显示以下负载测试的结果”中，选择要查看其结果的负载测试。 选择“\<Show results for all tests>”，以查看所有测试的全部结果。

     如果存在负载测试结果，它们将出现在“负载测试结果”列表中。 其中包括“时间”、“持续时间”、“用户”、“结果”、“测试”和“说明”列     。 “测试”列包含测试的名称，“说明”列包含运行测试之前添加的可选说明 。 “说明”列显示在“分析注释”中为此测试结果输入的简短说明 。

5. 在“负载测试结果”列表中，选择结果。 可以使用 Shift 键、Ctrl 键或者同时使用两者选择多个结果 。

6. 选择“移除”。

     结果已从储存库中移除。

    > [!NOTE]
    > 移除结果后“打开和管理负载测试结果”对话框仍然处于打开状态。

## <a name="see-also"></a>请参阅

- [如何：从存储库导出负载测试结果](../test/how-to-export-load-test-results-from-a-repository.md)
- [管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [如何：将负载测试结果导入存储库中](../test/how-to-import-load-test-results-into-a-repository.md)
