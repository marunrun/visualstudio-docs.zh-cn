---
title: 配置负载测试运行设置
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, configuring run settings
ms.assetid: 0c86918b-cd63-4468-8f49-6d547a1276dc
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 751dda344f65160fc76a528380d1f61e2cae5bec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62784125"
---
# <a name="configure-load-test-run-settings"></a>配置负载测试运行设置

“运行设置”是一组会影响负载测试运行方式的属性。 在“属性”窗口中，运行设置按类别进行组织。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

负载测试中可以有多个运行设置，但是每次运行时只可有一个运行设置处于活动状态。 其他运行设置提供了一个快速方法来选择备用设置，以用于后续的测试运行。

使用“新建负载测试向导”创建负载测试时，会创建初始运行设置。

![负载测试运行设置](../test/media/loadtestrunsettings.png)

## <a name="tasks"></a>任务

|任务|相关主题|
|-|-|
|**向负载测试添加更多运行设置：** 除了运行“新建负载测试向导”时创建的运行设置之外，还可向负载测试添加更多运行设置以便能够在不同条件下运行测试。|-   [如何：向负载测试添加额外的运行设置](../test/how-to-add-additional-run-settings-to-a-load-test.md)|
|**指定要用于负载测试的活动的运行设置：** 可以使用负载测试编辑器来选择要用于负载测试的运行设置。 活动的运行设置将由“[Active]”后缀标识。|-   [如何：为负载测试选择活动运行设置](../test/how-to-select-the-active-run-setting-for-a-load-test.md)|
|**编辑运行设置属性：** 可以编辑诸如日志记录选项等内容的运行设置属性（有关详细信息，请查看以下内容），来确定测试的长度、预热持续时间、报告错误详细信息的最大数量、采样率、连接模型（仅 Web 性能测试）、结果存储类型、验证级别和 SQL 跟踪。 运行设置应当体现负载测试的目标。|-   [负载测试运行设置属性](../test/load-test-run-settings-properties.md)<br />-   [更改运行设置属性](../test/load-test-run-settings-properties.md#change-run-setting-properties)|
|**在负载测试运行设置中指定测试迭代计数：** 可以通过配置“测试迭代”属性来指定在所有负载测试方案中运行所有 Web 性能测试和单元测试的次数。|-   [如何：在运行设置中指定测试迭代次数](../test/how-to-specify-the-number-of-test-iterations-in-a-load-test.md)|
|**为负载测试运行设置指定采样率：** 可以通过配置“采样率”属性来指定负载测试收集性能计数器数据的频率。|-   [如何：指定采样率](../test/how-to-specify-the-sample-rate-for-a-load-test.md)|
|**指定计时详细信息存储选项：** 可以通过配置“计时详细信息存储”属性来指定希望如何保存负载测试的详细信息。|-   [如何：指定计时详细信息存储属性](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md)|
|**指定测试资源保留期：** 通过设置“资源保留期”属性在指定期间内保留测试资源，从而加快测试 > 修复 > 重测循环。|-   [保留资源以加快负载测试](/azure/devops/test/load-test/getting-started-with-performance-testing?view=vsts)|
|**使用上下文参数：** 可以使用上下文参数来参数化字符串。 例如，如果负载测试中包含使用参数化 Web 服务器的 Web 性能测试，则可以向映射到不同服务器的运行设置中添加上下文参数。|-   [如何：向运行设置中添加上下文参数](../test/how-to-add-context-parameters-to-a-load-test-run-setting.md)|
|**配置测试日志记录属性：** 可以配置将与负载测试运行设置关联的数据写入日志的频率。 这在运行大型或复杂负载测试时很有用，因为该日志的大小可能会达到数个 GB。<br /><br /> 还可以将日志文件配置为在负载测试无法帮助调试和分析应用程序时自动保存。|-   [修改负载测试记录设置](../test/modify-load-test-logging-settings.md)|