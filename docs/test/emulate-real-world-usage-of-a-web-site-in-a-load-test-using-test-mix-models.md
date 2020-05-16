---
title: 在负载测试中模拟网站的实际使用情况
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load model, specifying
- load test load model, specifying
ms.assetid: b7fae849-0538-40d1-ab35-2bb3a0fe4393
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 18e22cd151d8013a50e34a01757069dde9574e79
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589599"
---
# <a name="test-mix-models-overview"></a>测试组合模型概述

使用负载建模选项可更准确地预测正在进行负载测试的网站或应用程序的预期实际使用情况。 执行这种操作很重要，因为未基于准确负载模型的负载测试会生成误导性结果。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="test-mix-model-enhancements"></a>测试组合模型增强功能

使用负载测试编辑器或测试组合模型向导可以为负载测试方案指定下列类型的测试组合。 有关详细信息，请参阅[在方案中更改测试组合模型](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)。

你可以为负载测试方案指定以下测试组合模型选项之一：

-  基于总测试数：确定虚拟用户启动测试迭代时运行的 Web 性能或单元测试。 在负载测试结束时，运行特定测试的次数与分配的测试分布相匹配。 使测试组合基于 IIS 日志或生产数据中的事务百分比时，可使用此测试组合模型。 有关详细信息，请参阅[基于已启动测试数的百分比](#BasedOnTestsStarted)。

-  基于虚拟用户数：确定将运行特定 Web 性能或单元测试的虚拟用户的百分比。 在负载测试的任何时刻，运行特定测试的用户数都与分配的分布相匹配。 使测试组合基于运行特定测试的用户的百分比时，可使用此测试组合模型。 有关详细信息，请参阅[基于虚拟用户数的百分比](#PercentageBasedonVirtualUsers)。

-  基于用户节奏：在负载测试过程中，每个用户每小时按指定次数运行每个 Web 性能测试或单元测试。 如果希望虚拟用户在负载测试过程中以特定节奏运行测试，则可使用此测试组合模型。 有关详细信息，请参阅[速度测试组合](#PacingTestMix)。

    > [!TIP]
    > 何时选择“百分比测试组合”和“基于虚拟用户数的百分比”   ？ 如果测试组合中某些测试的持续时间明显长于其他测试，则这两个选项之间的区别便尤为重要。 在这种情况下，最好选择“基于虚拟用户数的百分比”  。 此选项可帮助避免运行测试过程中，过多用户运行长时间测试的可能性。 但是，如果测试都具有相似的持续时间，则可以更安全地选择“百分比测试组合”  。

-  基于顺序测试顺序：每个虚拟用户按照在方案中定义测试的顺序运行 Web 性能测试或单元测试。 虚拟用户可按此顺序连续循环运行测试，直到负载测试完成。 有关详细信息，请参阅[顺序](#SequentialOrder)。

### <a name="percentage-based-on-tests-started"></a><a name="BasedOnTestsStarted"></a> 基于已启动测试数的百分比

对于组合中的每个测试，可以指定一个百分比，它确定选择测试作为下一个要运行的测试的频率。 例如，可能将下列百分比值分配给三种测试：

- 测试 A (50%)

- 测试 B (35%)

- 测试 C (15%)

如果使用此设置，则下一个要启动的测试将基于分配的百分比。 执行此操作时不考虑当前运行每个测试的虚拟用户的数目。

### <a name="percentage-based-on-virtual-users"></a><a name="PercentageBasedonVirtualUsers"></a> 基于虚拟用户数的百分比
此测试组合模型确定将运行特定测试的虚拟用户的百分比。 如果使用此测试组合模型，则下一个要启动的测试不仅基于分配的百分比，还基于当前运行特定测试的虚拟用户的百分比。 在负载测试的任何时刻，运行特定测试的用户数与分配的分发项尽可能匹配。

### <a name="pacing-test-mix"></a><a name="PacingTestMix"></a> 速度测试组合

如果指定速度测试组合，则为测试组合中每个测试的每个虚拟用户指定测试执行的速率。 对于每个测试，此速率是指每个虚拟用户每小时运行的测试数。 例如，可能将下列速度测试组合分配给以下测试：

- 测试 A：每个用户每小时 4 个测试

- 测试 B：每个用户每小时 2 个测试

- 测试 C：每个用户每小时 0.125 个测试

如果使用速度测试组合模型，则负载测试运行时引擎可保证测试启动的实际速率小于或等于指定的速率。 如果测试为完成分配的数目而运行时间太长，则会返回错误。

当使用速度测试组合时，“测试迭代之间的思考时间”设置将不适用  。

#### <a name="apply-distribution-to-pacing-delay"></a>对节奏延迟应用分布
负载测试方案中“对节奏延迟应用分布”属性的值可以设置为 true 或 false  ：

-  True：方案将应用“编辑测试组合”  对话框的“每个用户每小时的测试数”  列中的值指定的典型统计分布延迟。 有关详细信息，请参阅[编辑文本组合模型以指定运行测试的虚拟用户的概率](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)。

   例如，假定你将测试的“编辑测试组合”  对话框中的“每个用户每小时的测试数”  值设置为每小时 2 个测试。 如果“对节奏延迟应用分布”属性设置为“True”，则会将典型统计分布应用于测试之间的等待时间   。 用户每小时仍将运行 2 个测试，但是两次测试之间不一定要间隔 30 分钟。 第一个测试可以在 4 分钟后运行，第二个测试可以在 45 分钟后运行。

-  False：测试将以你为“编辑测试组合”  对话框的“每个用户每小时的测试数”  列中的值指定的特定节奏运行。 有关详细信息，请参阅[编辑文本组合模型以指定运行测试的虚拟用户的概率](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)。

   例如，假定你将测试的“编辑测试组合”  对话框中的“每个用户每小时的测试数”  值设置为每小时 2 个测试。 如果“对节奏延迟应用分布”属性设置为“False”，则测试运行时基本上没有机动时间   。 测试的运行间隔将为 30 分钟。 这样可以确保每小时执行 2 个测试。

  有关详细信息，请参阅[如何：在使用用户节奏测试组合模型时对节奏延迟应用分布](../test/how-to-apply-distribution-to-pacing-delay-when-using-a-user-pace-test-mix-model.md)。

### <a name="sequential-order"></a><a name="SequentialOrder"></a> 顺序
如果选择“基于顺序测试顺序”选项，则每个虚拟用户将按照测试的定义顺序运行方案中的所有测试。

## <a name="test-iterations-property"></a>“测试迭代”属性
在“运行设置”属性中，可以为“测试迭代”属性指定值。 此值是要在负载测试中运行的测试迭代的数目。 启动了指定数目的测试迭代后，将不再启动任何其他的测试迭代，而不管任何负载配置文件的设置。 完成了指定数目的测试迭代后，负载测试将结束。 有关详细信息，请参阅[如何：在运行设置中指定测试迭代数](../test/how-to-specify-the-number-of-test-iterations-in-a-load-test.md)。

## <a name="initialize-and-terminate-tests"></a>初始化测试和终止测试
可以选择要在每个虚拟用户的负载测试会话的开始和结束时运行的测试。 有关详细信息，请参阅[编辑文本组合模型以指定运行测试的虚拟用户的概率](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)。

- 初始化测试  。 在测试组合中的任何测试运行之前将由每个虚拟用户运行此测试。

- 终止测试  。 此测试在某个特定虚拟用户的所有测试运行后运行。

  请注意下列有关初始化测试和终止测试的信息：

- 可以按时间（而不是迭代计数）指定负载测试的持续时间。 在这种情况下，当负载测试的运行持续时间完成后，将不会运行终止测试。

- 如果初始化测试是单元测试或 Web 性能测试，将在初始化测试完成之后保存 TestContext 或 WebTestContext 对象的状态。 然后，它将用作测试组合中的测试迭代的启动上下文。

- 新的用户（如在“新用户的百分比”方案属性中定义的用户）总是执行初始化测试、测试组合中的某个测试的一次迭代和终止测试。

## <a name="see-also"></a>另请参阅

- [编辑文本组合模型以指定运行测试的虚拟用户的概率](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)
- [编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)
- [编辑测试组合以指定在负载测试方案中包括的测试](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)
- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
- [在方案中更改测试组合模型](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)
