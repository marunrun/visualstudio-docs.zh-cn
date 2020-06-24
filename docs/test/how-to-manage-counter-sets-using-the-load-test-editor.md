---
title: 负载测试计数器集
ms.date: 10/19/2016
ms.topic: how-to
f1_keywords:
- vs.test.load.dialog.countersetmapping
helpviewer_keywords:
- counters, counter sets
- performance counters
- counter sets
- load tests, counter sets
ms.assetid: 64315c2f-a0b2-4378-be16-0774b99beef5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1eeb99d58a9fc0547d118c529878d8b02cc83dda
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287683"
---
# <a name="how-to-manage-counter-sets-using-the-load-test-editor"></a>如何：使用负载测试编辑器管理计数器集

在使用“新建负载测试向导”创建负载测试时，需添加一个初始计数器集  。 该计数器集为您的负载测试提供了一组预定义计数器集。

> [!NOTE]
> 如果负载测试分布在多台远程计算机之间，则会将控制器和代理计数器映射到控制器和代理计数器集中。 有关如何在负载测试中使用远程计算机的详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

管理计数器集包括选择要从中收集性能数据的计算机集，指定从各个计算机收集数据的计数器集。 在“负载测试编辑器”中管理计数器  。

![管理计数器集](../test/media/loadtestmanagecountersets.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-manage-counter-sets"></a>管理计数器集

1. 打开一个负载测试。

2. 选择“管理计数器集”按钮  。

     \- 或 -

     右击负载测试树中的“计数器集”文件夹，然后选择“管理计数器集”   。

     随即显示“管理计数器集”对话框  。

3. （可选）在“选定的计算机和计数器集将添加到以下运行设置下”列表框中，选择其他运行设置  。

    > [!NOTE]
    > 这仅适用于负载测试中具有多个运行设置时。

4. （可选）选择“添加计算机”以添加要监视的新的计算机  。 系统会提示您输入名称。 键入计算机的名称，您将在新项下面看到节点。 例如，“ASP.NET”、“IIS”、“SQL”等    。 选中您要选择的节点前面的复选框。 新的计数器将出现在“预览选定内容”窗格中  。

5. （可选）在“计算机标记”文本框中，键入要与计算机关联的标记  。 例如，“TestMachine12 in lab3”。

     通过计算机标记可以用很容易识别的名称来标识计算机。

     在负载测试编辑器中，这些标记会显示在树的“计数器集映射”节点中  。 更重要的是，这些标记可显示在 Excel 报表中，从而帮助利益干系人标识计算机在负载测试中所具有的角色。 例如，“Web Server1 in lab2”或“SQL Server2 in Phoenix office”。 有关详细信息，请参阅[报告负载测试结果以比较测试或进行趋势分析](../test/compare-load-test-results.md)。

6. 选择 **“确定”** 。

## <a name="see-also"></a>另请参阅

- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)
- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
