---
title: 编辑测试组合模型
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, scenarios
- load tests, virtual users
ms.assetid: e3b7d952-9012-400a-8131-3444390a6066
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8ce54af89164b1a71c7328d04635c8735eec1b28
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288645"
---
# <a name="edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test"></a>编辑测试组合模型以指定运行测试的虚拟用户的概率

测试组合模型指定虚拟用户在负载测试方案中运行指定测试的概率。  这样可以更逼真地模拟负载。 应用程序可以有多个工作流而不是只得有一个，这样可以更逼真地模拟最终用户与应用程序的交互方式。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="test-mix-model-options"></a>测试组合模型选项

你可以为负载测试方案指定以下测试组合模型选项之一：

-  基于总测试数：确定虚拟用户启动测试迭代时运行的 Web 性能或单元测试。 在负载测试结束时，运行特定测试的次数与分配的测试分布相匹配。 使测试组合基于 IIS 日志或生产数据中的事务百分比时，可使用此测试组合模型。

-  基于虚拟用户数：确定将运行特定 Web 性能或单元测试的虚拟用户的百分比。 在负载测试的任何时刻，运行特定测试的用户数都与分配的分布相匹配。 使测试组合基于运行特定测试的用户的百分比时，可使用此测试组合模型。

-  基于用户节奏：在负载测试过程中，每个用户每小时按指定次数运行每个 Web 性能测试或单元测试。 如果希望虚拟用户在负载测试过程中以特定节奏运行测试，则可使用此测试组合模型。

-  基于顺序测试顺序：每个虚拟用户按照在方案中定义测试的顺序运行 Web 性能测试或单元测试。 虚拟用户可按此顺序连续循环运行测试，直到负载测试完成。

## <a name="tasks"></a>任务

|任务|相关主题|
|-|-----------------------|
| 为负载测试指定测试组合：创建负载测试时，可以在“新建负载测试向导”  中指定负载测试的设置。 在“新建负载测试向导”  中，选择要添加到初始方案中的现有 Web 测试和单元测试。 将测试添加到方案中之后，为方案指定测试组合。<br /><br /> 使用负载建模选项可更准确地预测正在进行负载测试的网站或应用程序的预期实际使用情况。 执行这种操作很重要，因为未基于准确负载模型的负载测试会生成误导性结果。|-   [模拟网站或应用程序的预期实际使用情况](../test/emulate-real-world-usage-of-a-web-site-in-a-load-test-using-test-mix-models.md)|
| 编辑测试组合模型：使用“负载测试编辑器”  可以更改负载测试方案，使其使用测试组合模型之一。||
|**为用户控制节奏的测试组合模型配置节奏延迟：** 如果负载测试方案配置为使用“基于用户节奏测试组合模型”，则可指定希望的配置分布节奏延迟的方式。 |-   [如何：在使用用户节奏测试组合模型时对节奏延迟应用分布](../test/how-to-apply-distribution-to-pacing-delay-when-using-a-user-pace-test-mix-model.md)|

## <a name="change-the-test-mix-model-in-a-scenario"></a>在方案中更改测试组合模型

在使用“新建负载测试向导”创建负载测试后，可以使用“负载测试编辑器”更改方案属性，以满足你的测试需求和目标。  

> [!NOTE]
> 有关负载设置属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

利用“负载测试编辑器”，可以通过在“属性”窗口中编辑“测试组合类型”属性来更改负载测试方案中的测试组合模型。

### <a name="to-change-the-test-mix-model"></a>更改测试组合模型

1. 打开一个负载测试。

     此时将显示“负载测试编辑器”  。 其中显示负载测试树。

2. 在负载测试树的“方案”文件夹中，选择要为其指定最大测试迭代次数的方案节点。 

3. 在“视图”菜单上选择“属性”窗口。  

     将显示该方案的类别和属性。

4. 在“测试组合类型”属性中，选择省略号按钮（“…”）。  

     随即出现“编辑测试组合”对话框。 

5. 选择“测试组合模型”下的下拉列表并选择要用于方案的测试组合模型。 

6. （可选）使用“添加”、“删除”和“分布”按钮及分布滑动条来修改测试组合。    有关详细信息，请参阅[编辑测试组合以指定在负载测试方案中包括的测试](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)。

7. （可选）通过使用复选框和选择所需测试指定要初始化或结束的 Web 性能测试和单元测试。 有关详细信息，请参阅[模拟网站或应用程序的预期实际使用情况](../test/emulate-real-world-usage-of-a-web-site-in-a-load-test-using-test-mix-models.md)。

8. 选择 **“确定”** 。

     “属性”窗口显示用于“测试组合类型”属性的新测试组合模型。  

9. 更改属性后，在“文件”菜单上选择“保存”。   然后，可以用新的“测试组合类型”值运行负载测试。 

## <a name="see-also"></a>另请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
