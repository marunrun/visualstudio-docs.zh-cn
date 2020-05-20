---
title: 导出负载测试结果
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- results, load test
- load tests, exporting results
- Load Test Results Repository
- load test results, exporting
ms.assetid: 716c2af5-8737-4d31-956f-a0273f7c5c0c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f72dbd687bc9177cd4cfd36416acb23445d30c8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589040"
---
# <a name="how-to-export-load-test-results-from-a-repository"></a>如何：从存储库导出负载测试结果

运行负载测试时，在运行期间收集的信息都存储到负载测试结果储存库中。 负载测试结果储存库中包含性能计数器数据和有关任何错误的信息。 有关详细信息，请参阅[管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)。

可以使用“打开和管理负载测试结果”对话框，从“负载测试编辑器”中管理负载测试结果。  您可以打开、导入、导出和移除负载测试结果。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-export-results-from-a-repository"></a>从储存库中导出结果

1. 从 Web 性能和负载测试项目中，打开负载测试。

2. 在嵌入式工具栏上，选择  “打开和管理结果”。

     随即出现  “打开和管理负载测试结果”对话框。

3. 在“请输入要用来查找负载测试结果的控制器名称”中选择一个控制器  。 选择“\<本地 - 无控制器>”以访问本地存储的结果。

4. 在“显示以下负载测试的结果”中，选择要查看其结果的负载测试  。 选择“\<显示所有测试的结果>”以查看所有测试的所有结果。

     如果存在负载测试结果，它们将出现在“负载测试结果”列表中  。 其中包括“时间”、“持续时间”、“用户”、“结果”、“测试”和“说明”列。       “测试”列包含测试的名称，“说明”列包含运行测试之前添加的可选说明。   “说明”列显示在“分析注释”中为此测试结果输入的简短说明   。

5. 在“负载测试结果”列表中，选择结果  。 可以使用 Shift 键、Ctrl 键或同时使用这两个键来选择多个结果，并将它们导出到单个文件中   。

6. 选择“导入”  。

     随即出现“导出负载测试结果”对话框  。

7. 在“文件名”框中，键入一个名称，然后选择“保存”   。

     结果即导出到一个存档文件中。

    > [!NOTE]
    > 出现结果后“打开和管理负载测试结果”对话框仍然处于打开状态  。

## <a name="see-also"></a>另请参阅

- [管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [如何：从存储库中删除负载测试结果](../test/how-to-delete-load-test-results-from-a-repository.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [如何：将负载测试结果导入存储库中](../test/how-to-import-load-test-results-into-a-repository.md)
