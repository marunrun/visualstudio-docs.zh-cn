---
title: 指定要在负载测试方案中使用的测试代理
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- test agents, load tests
- load tests, scenarios
- load tests, specifying for load tests
- tests agents, load tests, specifying
- load tests, test agents
ms.assetid: e86806dd-5897-4e4c-bfd4-8d687fb72a6e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d23d565752d81bff960027090ddaaf88e9d78ed5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588923"
---
# <a name="how-to-specify-test-agents-to-use-in-load-test-scenarios"></a>如何：指定要在负载测试方案中使用的测试代理

在使用“新建负载测试向导”创建负载测试后，可以使用“负载测试编辑器”更改方案属性，以满足测试需求和目标   。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

使用负载测试编辑器更改“属性”窗口中的“要使用的代理”属性可指定代理    。

如果要使用控制器和代理来远程运行负载测试，则可以指定希望方案使用的代理。 例如，你可能希望指定一组特定的代理，以便在分析性能趋势时保持一致性。 此外，还可以按地理位置分布各代理，以便代理运行的脚本和代理所在的位置之间存在关联。

> [!TIP]
> 另一种方法不需要代理的实际地理位置在远程站点，而是使用网络仿真来模拟慢速网络。 有关详细信息，请参阅[指定虚拟网络类型](../test/specify-virtual-network-types-in-a-load-test-scenario.md)。

有关详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

另一个原因是某些代理（并非全部）可能安装了某个特定方案所需的软件。

可以使用测试设置中的角色控制给定测试运行的代理选择。 有关详细信息，请参阅[使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)。

如果测试代理计算机的 CPU 使用率超过 75% 或可用物理内存不到 10%，请向负载测试添加更多代理以确保代理计算机不会成为负载测试的瓶颈。

## <a name="to-specify-the-agents-to-use-for-a-scenario"></a>指定要用于方案的代理

1. 打开一个负载测试。

     “负载测试编辑器”随即显示  。 其中显示负载测试树。

2. 在负载测试树的“方案”文件夹中，选择要为其指定所用代理的方案节点  。

3. 在“视图”菜单上选择“属性窗口”   。

     该方案的类别和属性将显示在“属性”窗口中  。

4. 在与“要使用的代理”属性对应的文本框中，键入该方案可运行于的代理的列表  。

     代理必须用逗号分隔，例如“Agent1, Agent2, Agent3”  。 将该属性保留为空白会指定该方案应使用所有可用的代理。

    > [!NOTE]
    > 对本地运行将忽略“要使用的代理”属性  。 对于远程运行，如果“要使用的代理”中指定的代理都不存在，则该方案中的测试将不运行  。

5. 更改属性后，在“文件”菜单上选择“保存”   。 然后，就可以用新的“要使用的代理”值运行负载测试了  。

## <a name="see-also"></a>请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [演练：创建和运行负载测试](../test/walkthrough-create-and-run-a-load-test.md)
- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
