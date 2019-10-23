---
title: 负载测试方案属性
ms.date: 10/19/2016
ms.topic: reference
helpviewer_keywords:
- load tests, properties
- load tests, scenarios
ms.assetid: 4414a638-1fa2-40ad-b1f4-b99f90b62e62
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 54159ca7b0d99e0bba7e7b048138ffacf6ab5b0b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652958"
---
# <a name="load-test-scenario-properties"></a>负载测试方案属性

可在 Visual Studio 中更改负载测试方案属性设置以满足负载测试要求。 本文按类别列出了各种负载测试方案属性。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="general"></a>常规

|属性|定义|
|-|----------------|
|**Name**|方案的名称。|

## <a name="mix"></a>组合

|属性|定义|
|-|----------------|
|**浏览器组合**|指定负载测试的 Web 浏览器组合。 可以指定不同的 Web 浏览器类型及其负载分布。<br /><br />选择省略号 (…) 按钮以打开“编辑浏览器组合”对话框，并使用“添加”和“删除”来选择负载测试中的 Web 浏览器类型     。<br /><br />有关详细信息，请参阅[指定 Web 浏览器类型](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)。|
|**网络组合**|指定负载测试的网络组合。 可以指定要包括的网络类型及其负载分布。<br /><br />选择省略号 (…) 按钮以打开“编辑网络组合”对话框，并使用“添加”和“删除”来选择负载测试中的网络类型     。<br /><br />有关详细信息，请参阅[指定虚拟网络类型](../test/specify-virtual-network-types-in-a-load-test-scenario.md)。|
|**测试组合**|指定负载测试的 Web 性能和单元测试组合。 可以指定要包括的测试及其负载分布。<br /><br />选择省略号 (…) 按钮以打开“编辑测试组合”对话框，并使用“添加”和“删除”来选择负载测试中的测试     。<br /><br />有关详细信息，请参阅[编辑负载测试方案的测试组合](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)。|
|**测试组合类型**|指定用于负载测试的测试组合模型。<br /><br />选择省略号 (…) 按钮以打开“编辑测试组合”对话框，并使用“测试组合模型”下的下拉列表来选择要在负载测试中使用的测试组合模型    。<br /><br />有关详细信息，请参阅[编辑测试组合模型](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)。|

## <a name="options"></a>选项

|属性|定义|
|-|----------------|
|**要使用的代理**|指定在远程运行负载测试时希望方案使用的代理。 例如，你可能希望指定一组特定的代理，以便在分析性能趋势时保持一致性。 此外，还可以按地理位置分布各代理，以便代理运行的脚本和代理所在的位置之间存在关联。<br /><br />代理必须用逗号分隔，例如“Agent1, Agent2, Agent3”  。 将该属性保留为空白会指定该方案应使用所有可用的代理。<br /><br />有关详细信息，请参阅[如何：指定要使用的测试代理](../test/how-to-specify-test-agents-to-use-in-load-test-scenarios.md)。|
|**对节奏延迟应用分布**|该布尔值用于指定是否要在用户节奏测试组合模型中应用典型分布延迟。 此属性仅在“测试组合类型”属性设置为“基于用户节奏”时适用   。<br /><br />有关详细信息，请参阅[如何：对节奏延迟应用分布](../test/how-to-apply-distribution-to-pacing-delay-when-using-a-user-pace-test-mix-model.md)|
|**IP 切换**|该布尔值用于指定是否使用 IP 切换。<br /><br />IP 切换使测试代理可以使用一些不同的 IP 地址向服务器发送请求。 这模拟了来自不同客户端计算机的调用。 针对负载平衡的 Web 场进行测试时，IP 切换很重要。 大多数负载均衡器通过使用客户端的 IP 地址在客户端与特定的 Web 服务器之间建立关联。 如果所有请求看上去都来自单个客户端，则负载平衡器不会平衡负载。 若要在 Web 场中实现较好的负载平衡，请求来自某个范围内的 IP 地址很重要。<br /><br />IP 切换仅适用于测试代理。|
|**最大测试迭代数**|该数值用于指定要在方案中运行的最大测试次数。 值 0 表示未指定最大次数。<br /><br />有关详细信息，请参阅[为方案配置测试迭代](../test/configure-test-iterations-in-a-load-test-scenario.md)。|
|**新用户的百分比**|该数值用于指定方案中的新用户或者首次访问者所占的百分比。<br /><br />有关详细信息，请参阅[如何：指定使用 Web 高速缓存数据的虚拟用户的百分比](../test/how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data.md)。|
|**思考时间配置文件**|指定方案是否将使用“正态分布”，或者是“打开”还是“关闭”思考时间配置文件    。<br /><br />有关详细信息，请参阅[编辑思考时间以模拟网站上的人机交互延迟](../test/edit-think-times-in-load-test-scenarios.md)。|

## <a name="timing"></a>计时

|属性|定义|
|-|----------------|
|**延迟开始时间**|该时间值用于指示在负载测试开始后延迟启动方案的小时数、分钟数和秒数。 如果“预热过程中禁用”属性设置为“True”，则在预热期完成后将应用要等待的时间量   。<br /><br />有关详细信息，请参阅[配置方案启动延迟](../test/configure-scenario-start-delays.md)。|
|**预热过程中禁用**|该布尔值用于指定方案是否应在负载测试的运行设置中指定的“预热持续时间”属性时间值期间运行  。<br /><br />有关负载测试运行设置属性的详细信息，请参阅[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。<br /><br />有关详细信息，请参阅[配置方案启动延迟](../test/configure-scenario-start-delays.md)。|
|**测试迭代之间的思考时间**|该数值用于指定测试迭代之间的等待时间（以秒为单位）。<br /><br />有关详细信息，请参阅[编辑思考时间以模拟网站上的人机交互延迟](../test/edit-think-times-in-load-test-scenarios.md)。|

## <a name="see-also"></a>请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)