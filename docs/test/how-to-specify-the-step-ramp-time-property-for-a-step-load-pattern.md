---
title: 负载测试的单步负载模式的单步增加时间
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, load patterns
ms.assetid: 4a69e857-f93b-4907-9a01-fd1b66291205
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a40f7ce4aacfdc03b5e05becbfc83439945f7e8a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75588910"
---
# <a name="how-to-specify-the-step-ramp-time-property-for-a-step-load-pattern"></a>如何：为分级负载模式指定单步负载增加时间属性

在用“新建负载测试向导”创建负载测试之后，可以使用“负载测试编辑器”来更改方案属性以满足测试需求和目标   。 有关详细信息，请参阅[演练：创建和运行负载测试](../test/walkthrough-create-and-run-a-load-test.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

在“属性”窗口中设置“单步负载增加时间”属性   。 在负载测试编辑器中编辑负载测试方案属性  。

“单步负载增加时间”属性仅用于分级负载模式  。 有关详细信息，请参阅[编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)。

分级负载模式用于在负载测试运行时增加服务器上的负载，这样您就能够看到性能如何随着用户负载的增加而发生变化。 例如，若要查看用户负载增加到 2000 个用户时服务器的性能如何，您可以使用具有以下属性的分级负载模式来运行一个 10 小时的负载测试：

- 初始用户计数：100

- 最大用户计数：2000

- 单步持续时间(秒)：1800

- 单步负载增加时间(秒)：20

- 单步用户计数：100

这些设置可使负载测试在 100、200、300 直至 2000 个用户的用户负载下运行 30 分钟（1800 秒）。

> [!NOTE]
> “单步负载增加时间”属性是这些属性中唯一无法在“新建负载测试向导”中选择的属性   。

通过“单步负载增加时间”属性，可从某一步逐渐增加到下一步（例如，从 100 个用户增加到 200 个用户）而不是立即增加  。 在此示例中，用户负载将在 20 秒内从 100 个用户增加到 200 个用户，即每秒增加 5 个用户。

## <a name="to-edit-the-step-ramp-time-property-for-a-step-load-pattern"></a>编辑分级负载模式的“单步负载增加时间”属性

1. 打开一个负载测试。

     此时将显示“负载测试编辑器”  。 其中显示负载测试树。

2. 在负载测试树的“方案”文件夹中，打开要为其指定单步负载增加时间的方案节点  。

3. 选择“分级负载模式”节点  。

    > [!NOTE]
    > 该方案的负载模式必须是分级负载模式。 如果不是，则负载模式将显示当前与该方案关联的负载模式类型。 有关详细信息，请参阅[编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)。

4. 在“视图”菜单上选择“属性”窗口。  

     该方案的类别和属性将显示在“属性”  窗口中。

5. 通过输入每一步所占用的秒数来设置“单步负载增加时间”属性的值，以逐渐添加由“单步用户计数”属性所指定的用户   。

6. 更改完此属性后，请选择“文件”菜单上的“保存”。   然后，可以使用新的“单步负载增加时间”值运行负载测试  。

## <a name="see-also"></a>另请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
- [编辑负载模式以便为虚拟用户活动建模](../test/edit-load-patterns-to-model-virtual-user-activities.md)
