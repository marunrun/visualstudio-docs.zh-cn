---
title: 为负载测试配置测试迭代
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios, iterations
- load test, iterations
- load tests, scenarios
ms.assetid: ac480fb7-f4f7-47dc-9ae5-98be3aca4fba
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e95ca27ace50c7b28d1ffb1d3fc02589daddee2d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590977"
---
# <a name="configure-test-iterations-in-a-load-test-scenario"></a>在负载测试方案中配置测试迭代

若要配置测试迭代设置，请使用负载测试编辑器和“属性”窗口编辑负载测试方案  。 负载测试方案的默认设置不指定最大测试迭代数。 您可以选择配置方案中的最大迭代数以及它们之间的暂停时间。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="specify-the-maximum-test-iterations-for-a-scenario"></a>为方案指定最大测试迭代数

通过使用负载测试编辑器在“属性”窗口中更改“最大测试迭代数”属性，可以指定要为某一方案运行测试的最大次数   。

“最大测试迭代数”属性可控制要为方案运行的测试迭代的最大次数。  如同负载测试运行设置中的“测试迭代”属性一样，这是所有代理上所有用户的最大数，而不是针对单个用户的设置。 

> [!NOTE]
> 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

对于顺序测试组合，一次迭代要遍历该组合中的所有测试。 对于所有其他测试组合，每次测试执行算作一次迭代。 有关详细信息，请参阅[关于混合控件](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)。

如果该负载测试是基于持续时间的负载测试，并且在完成迭代次数之前持续时间已满，则该测试仍将停止。 如果该测试是基于迭代的测试，并且在完成方案迭代次数之前即已完成测试迭代次数，则该测试将停止。 使用与负载测试中的运行设置关联的“属性”窗口中的“运行持续时间”属性，可设置持续时间   。

完成方案迭代次数时，该方案将停止运行，但所有其他活动方案将继续运行。

> [!NOTE]
> 相关属性为 Web 测试数据源上的“唯一”属性，使用该属性将依次历经整个数据，但每个记录仅历经一次。  有关详细信息，请参阅[将数据源添加到 Web 性能测试](../test/add-a-data-source-to-a-web-performance-test.md)。

“最大测试迭代数”属性在多种情况下都很有用。  有些负载测试人员更愿意执行基于迭代的测试，而另一些负载测试人员更愿意执行基于持续时间的测试。

![指定方案中的测试迭代数](../test/media/loadtest_prop.png)

### <a name="to-specify-the-maximum-test-iterations"></a>指定最大测试迭代数

1. 打开一个负载测试。

2. 此时将显示负载测试编辑器。 其中显示负载测试树。

3. 在负载测试树的“方案”文件夹中，选择要为其指定最大测试迭代数的方案节点。 

4. 在“视图”菜单上选择“属性”窗口。  

     该方案的类别和属性将显示在“属性”窗口中  。

5. 在“最大测试迭代数”属性文本框中，键入指示在运行负载测试时该方案要运行的最大测试次数。 

    > [!NOTE]
    > “最大测试迭代数”属性的值为 0 则指定没有最大迭代次数。 

6. 更改完此属性后，请选择“文件”菜单上的“保存”。   然后，可以使用新的“最大测试迭代数”值运行负载测试。 

## <a name="specify-think-times-between-test-iterations-for-a-scenario"></a>为方案指定测试迭代之间的思考时间

“测试迭代之间的思考时间”属性是在负载测试编辑器中编辑负载测试方案属性时使用“属性”窗口设置的   。

“测试迭代之间的思考时间”属性用于指定开始测试迭代前等待的秒数。 

> [!NOTE]
> 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

### <a name="to-specify-the-think-time-between-test-iterations"></a>指定测试迭代之间的思考时间

1. 打开一个负载测试。

     此时将显示“负载测试编辑器”  。 其中显示负载测试树。

2. 在负载测试树的“方案”  文件夹中，选择要为其指定思考时间的方案节点。

3. 在“视图”菜单上选择“属性”窗口。  

     该方案的类别和属性将显示在“属性”  窗口中。

4. 在“测试迭代之间的思考时间”属性的值中输入一个数字，该数字表示开始下一个测试迭代之前需要等待的秒数。 

5. 更改完此属性后，请选择“文件”菜单上的“保存”。   然后，可以使用新的“测试迭代之间的思考时间”值运行负载测试。 

## <a name="see-also"></a>另请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [为负载测试配置测试代理和测试控制器](../test/configure-test-agents-and-controllers-for-load-tests.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
- [编辑思考时间以模拟网站人工交互延迟](../test/edit-think-times-in-load-test-scenarios.md)
