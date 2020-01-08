---
title: 创建和运行负载测试
ms.date: 10/01/2016
ms.topic: conceptual
helpviewer_keywords:
- unit tests, in load tests
- unit tests, load test walkthrough
- load tests, walkthrough
ms.assetid: bbf075a5-96d5-48ed-a03c-330f0fc04748
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1c2ade11d4bffc3c9fdf812cb38d21cd742c9845
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590847"
---
# <a name="walkthrough-create-and-run-a-load-test-that-contains-unit-tests"></a>演练：创建并运行包含单元测试的负载测试

在本演练中将创建一个包含单元测试的负载测试。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

本演练将引导你使用 Visual Studio Enterprise 来完成负载测试的创建和运行过程。 负载测试是 Web 性能测试和单元测试的容器。 可以使用“新建负载测试向导”创建负载测试  。

负载测试还公开许多运行时属性，可以对这些属性加以修改以生成所需的负载模拟。 在本演练中，将使用“新建负载测试向导”向负载测试中添加单元测试  。

在本演练中，你将完成以下任务：

- 创建使用单元测试的负载测试。

- 更改一些负载测试设置。

- 运行负载测试。

- 执行[演练：为托管代码创建和运行单元测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)中的步骤，以创建一个简单的 C# 类库，该类库包含具有若干单元测试的 Web 性能和负载测试项目。

## <a name="create-a-load-test-containing-unit-tests-using-the-new-load-test-wizard"></a>使用“新建负载测试向导”创建包含单元测试的负载测试

### <a name="to-start-the-new-load-test-wizard"></a>启动“新建负载测试向导”

1. 打开在[演练：创建并运行托管代码的单元测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)中创建的 Bank 解决方案。

2. 在“解决方案资源管理器”中，打开 Bank 解决方案节点的快捷菜单，选择“添加”，然后选择“新建项目”    。

     此时，将显示“添加新项目”对话框  。

3. 在“添加新项目”对话框中，展开“Visual C#”，然后选择“测试”    。 从模板列表中，选择“Web 性能和负载测试项目”，并在“名称”字段中键入 `BankLoadTest`   。 选择 **“确定”** 。

     BankLoadTest Web 性能测试和负载测试项目将添加到解决方案中。

4. 打开新的 BankLoadTest Web 性能和负载测试项目的快捷菜单，选择“添加”，然后选择“负载测试”   。

5. 启动“新建负载测试向导”  。

6. “欢迎使用”页是“新建负载测试向导”的第一页   。

7. 选择“下一步”  。

### <a name="to-edit-settings-for-load-test-scenario"></a>编辑负载测试方案的设置

1. 在“输入负载测试方案的名称”文本框中，键入“ScenarioSample”   。

     “方案”是一种分组机制  。 它由一组测试和用于在负载下运行这些测试的属性组成。

2. 将“思考时间配置文件”  设置为 `Use normal distribution centered on recorded think times`。 思考时间表示用户在继续下个网页之前思考网页的时间。

1. 完成后选择“下一步”  。

### <a name="to-edit-load-pattern-setting-for-test-scenario"></a>编辑测试方案的负载模式设置

1. 选择“分级负载”  。

    > [!NOTE]
    > 可以从两种负载模式中进行选择：常量负载和分级负载。 每一种负载模式在负载测试中都有其作用，但对于本演练，请选择“分级负载”  。

2. 将“开始用户计数”设置为 10 个用户  。

3. 将“单步持续时间”设置为 10 秒  。

4. 将“单步用户计数”设置为 10 个用户/步  。

5. 将“最大用户计数”设置为 100 个用户  。

6. 选择“下一步”  。

### <a name="to-select-test-mix-model-for-the-scenario"></a>为方案选择测试组合模型

1. 在“应如何对测试组合进行建模”下，选择“基于总测试数”   。

2. 选择“下一步”  。

### <a name="to-add-unit-tests-to-the-scenario"></a>向方案中添加单元测试

1. 下一步是“向负载测试方案中添加测试并编辑测试组合”  。

2. 选择“添加”来选择测试  。

3. 选择“可用测试”窗格中列出的 CreditTest 单元测试，该窗格列出了 Web 性能和负载测试项目中的所有 Web 性能测试和单元测试   。

4. 选择箭头将 CreditTest 单元测试添加到“选定的测试”窗格中   。

5. 对 DebitTest 和 FreezeAccountTest 单元测试重复步骤 3 和 4   。

6. 添加完这三个单元测试后，选择“确定”  。

     随即出现测试组合。

7. 将“分布”下 CreditTest 的滑块略微向右移动一些以调整测试分布   。 请注意，其他滑块会自动向左移动以便分布仍然保持 100%。

8. 选择“下一步”  。

### <a name="to-select-network-mix-for-test-scenario"></a>为测试方案选择网络组合

1. 选择局域网连接类型以添加到网络带宽组合中。

     此外，还可以添加其他网络类型。 使用滑块来调整测试分发和权重。

2. 选择“下一步”  。

### <a name="to-specify-computers-to-monitor-with-counter-sets-during-load-test-run"></a>指定在负载测试运行期间要使用计数器集监视的计算机

1. 选择“下一步”  。

     有关计数器集的详细信息，请参阅[为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)。

### <a name="to-edit-run-setting-for-load-test"></a>编辑负载测试的运行设置

1. 选择“负载测试持续时间”，然后将“运行持续时间”设置为 2 分钟，以便对负载测试执行冒烟测试    。

     生成负载测试时，最好通过运行一个短暂的小负载测试来验证是否一切都已正确配置并可按预期运行。 此过程称为“冒烟测试”  。

2. 选择“完成”  。 将在“负载测试编辑器”中打开负载测试  。

## <a name="run-the-load-test"></a>运行负载测试
 创建了负载测试后，请运行该测试以查看您的 Bank 应用程序如何响应负载模拟。 负载测试运行时，将看到“负载测试分析器”窗口  。

### <a name="to-run-the-load-test"></a>运行负载测试

1. 在“负载测试编辑器”中打开一个负载测试后，选择工具栏中“运行测试”绿色按钮   。 负载测试开始运行。

2. 如果测试模拟超过所有阈值，则树控件节点中将出现图标，以指示阈值冲突。 错误上覆盖着红色圆圈，而警告上覆盖着黄色三角形。 可以找出超过阈值的计数器，然后通过将图标拖动到关系图上来绘制该计数器。 可在测试运行期间执行此操作。

## <a name="see-also"></a>请参阅

- [编辑测试组合以指定在负载测试方案中包括的测试](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)
- [指定虚拟网络类型](../test/specify-virtual-network-types-in-a-load-test-scenario.md)
- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)
- [编辑文本组合模型以指定运行测试的虚拟用户的概率](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)
