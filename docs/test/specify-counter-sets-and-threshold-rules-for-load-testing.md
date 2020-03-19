---
title: 适用于负载测试的计数器集和阈值规则
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- counters, counter sets
- load tests, thresholds
- counter sets
- load tests, performance
- load tests, counter sets
- load tests, threshold rules
ms.assetid: 9e14d955-f3a4-4717-bbfe-7f08cdda5678
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 440bc01b52269c477d9d2f2194fd831041f1d20d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596315"
---
# <a name="specify-counter-sets-and-threshold-rules-for-computers-in-a-load-test"></a>为负载测试中的计算机指定计数器集和阈值规则

负载测试提供了命名计数器集，这些计数器集在分析性能计数器数据时十分有用。 这些计数器集按不同的技术组织在一起，包括“应用程序”、“ASP.NET”、“.NET 应用程序”、“IIS”和“SQL”。 在使用“新建负载测试向导”创建负载测试时，需添加一个初始计数器集  。 这些计数器为你提供了一组重要的、用于负载测试的预定义计数器。 在“负载测试编辑器”中管理计数器。 

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 如果负载测试分布在多台远程计算机之间，则会将控制器和代理计数器映射到控制器和代理计数器集中。 有关如何在负载测试中使用远程计算机的详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

在指定的计算机上收集计数器集。 计数器集与负载测试期间使用的计算机之间的关联就是计数器集映射  。 例如，所测试的 Web 服务器可能会具有 ASP.NET、IIS 和 .NET 应用程序计数器集映射。

默认情况下，在控制器和代理上收集性能计数器。 有关详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

您应将正在测试的服务器添加到需要收集其计数器的计算机的列表中，这一点很重要。 然后即可在负载测试期间收集和监视任何重要的系统数据。

## <a name="tasks"></a>任务

|任务|相关主题|
|-|-----------------------|
|**管理负载测试的计数器集：** 创建负载测试后，可以在负载测试编辑器中编辑计数器集。 管理计数器集包括选择要从中收集性能数据的计算机集，并指定用于从各个计算机收集数据的计数器集。 可在负载测试编辑器中管理计数器。|-   [如何：管理计数器集](../test/how-to-manage-counter-sets-using-the-load-test-editor.md)|
|**向负载测试添加计数器集：** 使用“新建负载测试向导”创建负载测试时，需添加一个初始计数器集。  该计数器集为您的负载测试提供了一组预定义计数器集。 创建负载测试后，可以使用负载测试编辑器向现有计数器集添加新的计数器。|-   [如何：向计数器集中添加计数器](../test/how-to-add-counters-to-counter-sets-using-the-load-test-editor.md)<br />-   [如何：添加自定义计数器集](../test/how-to-add-custom-counter-sets-using-the-load-test-editor.md)|
|**指定对负载测试应用计数器的相关阈值规则：** “阈值规则”即对单个性能计数器进行设置以在负载测试过程中监视系统资源使用情况的规则。 计数器集定义中包含有许多关键性能计数器的预定义阈值规则。 负载测试中的阈值规则将一个性能计数器值与一个常数值或另一个性能计数器值进行比较。|-   [如何：添加阈值规则](../test/how-to-add-a-threshold-rule-using-the-load-test-editor.md)|
|**将友好名称分配给计数器集映射到的计算机：** 可添加计算机标记，以便为计算机应用易于识别的名称。 在负载测试编辑器中，这些标记显示在树的“计数器集映射”节点中  。 更重要的是，这些标记将显示在 Excel 报表中，可以帮助利益干系人标识计算机在负载测试中的角色，例如“Web Server1 in lab2”或“SQL Server2 in Phoenix office”。<br /><br /> 有关详细信息，请参阅[报告负载测试结果以比较测试或进行趋势分析](../test/compare-load-test-results.md)。||

## <a name="use-counter-sets"></a>使用计数器集

负载测试工具会不断地使用计数器收集性能数据并绘制相应的图形。 在负载测试运行期间，将按用户指定的时间间隔收集计数器数据。 有关详细信息，请参阅[如何：指定采样率](../test/how-to-specify-the-sample-rate-for-a-load-test.md)。 使用负载测试分析器，可以在运行时查看计数器，或者在负载测试运行完成后查看计数器  。

将在服务器和任何运行测试的计算机上收集计数器数据。 如果设置了一组代理计算机来运行测试，则还将收集这些计算机上的计数器。

有三种计数器类别：百分比、计数和平均数。 这三种计数器类别的例子分别为：“% CPU usage”（CPU 使用百分比）、“SQL Server lock counts”（SQL Server 锁计数）和“IIS requests per second”（每秒的 IIS 请求数）。

![负载测试计数器集](../test/media/loadtestcountersets.png)

各个 HTTP 请求的性能数据由运行测试的计算机报告。 如代理计算机。 对于请求，可以监视“Average Time to First Byte”（收到第一个字节的平均时间）、“Response Time”（响应时间）和“Requests per Second”（每秒请求数）等数据。

为了便于在 Web 服务器上收集性能数据，Visual Studio Enterprise 还基于在负载测试中使用的技术提供了预定义的命名计数器集。 这些计数器集在您分析运行 IIS、ASP.NET 或 SQL Server 的服务器时很有用。 可以使用负载测试编辑器添加默认的计数器集中没有提供的计数器。 请务必将正在测试的计算机或服务器添加到负载测试中，以确保可以监视这些计算机上的资源使用情况。 有关详细信息，请参阅[如何：管理计数器集](../test/how-to-manage-counter-sets-using-the-load-test-editor.md)。

负载运行的结果分析经常要求您具备某个方面的专业知识，这样才能知道需要收集哪些数据、在哪些地方设置阈值规则以及如何判别测量值反映出的应用程序中的特定问题。 有关详细信息，请参阅[关于阈值规则](#about-threshold-rules)。

### <a name="performance-counter-sampling-interval-considerations"></a>性能计数器采样间隔注意事项

根据负载测试的长度，可在负载测试运行设置中为“采样速率”属性选择适当的值  。 较小的采样速率（如 5 秒默认值）需要占用负载测试结果数据库中的更多空间。 对于较长的负载测试，增加采样速率会减少收集的数据量。 有关详细信息，请参阅[如何：指定采样率](../test/how-to-specify-the-sample-rate-for-a-load-test.md)。

下面是有关采样速率的一些准则。

|负载测试持续时间|建议的采样速率|
|-|-----------------------------|
|\< 1 小时|5 秒|
|1 - 8 小时|15 秒|
|8 - 24 小时|30 秒|
|> 24 小时|60 秒|

## <a name="store-performance-data"></a>存储性能数据

在负载测试运行期间，将收集性能计数器数据并将其存储在负载测试结果存储库中  。 有关详细信息，请参阅[管理负载测试结果存储库中的负载测试结果](../test/manage-load-test-results-in-the-load-test-results-repository.md)。

## <a name="about-threshold-rules"></a>关于阈值规则

“阈值规则”即对单个性能计数器进行设置以在负载测试过程中监视系统资源使用情况的规则  。 计数器集定义中包含有许多关键性能计数器的预定义阈值规则。 有关详细信息，请参阅[使用计数器集帮助分析负载测试中的性能计数器数据](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)。

## <a name="threshold-rules-and-levels"></a>阈值规则和级别

在负载测试中创建阈值规则时，可以在两种规则中进行选择：

比较常数 &mdash; 比较性能计数器的值与常数值。

比较计数器 &mdash; 将一个性能计数器的值与另一个性能计数器的值进行比较。

在创建阈值规则时，还可以设置规则的等级。 等级即警告阈值和临界阈值。 在查看负载测试运行时，警告等级阈值冲突用一个黄色的符号表示，临界等级阈值冲突用一个红色的符号表示。

## <a name="the-alert-if-over-property"></a>“如果超过则发出警报”属性

将“如果超过则发出警报”属性设置为“True”，可指示超出阈值将出现问题   。 例如，如果对“% Processor Time”（处理器时间百分比(%)）设置阈值规则，并且希望值大于 90 时收到警报，请使用“比较常数”规则类型，将“临界阈值”设置为 90，并将“如果超过则发出警报”设置为“True”      。

将“如果超过则发出警报”属性设置为“False”，可指示低于阈值将出现问题   。 例如，如果对“Requests/Sec”（请求数/秒）设置阈值规则，并且希望值低于 50 时收到警报，请使用“比较常数”规则类型，将“临界阈值”设置为 50，并将“如果超过则发出警报”设置为“False”      。

## <a name="see-also"></a>请参阅

- [如何：添加阈值规则](../test/how-to-add-a-threshold-rule-using-the-load-test-editor.md)
- [分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)
