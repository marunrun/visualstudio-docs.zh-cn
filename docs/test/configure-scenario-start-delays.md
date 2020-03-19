---
title: 配置负载测试的方案启动延迟
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios, start delays
ms.assetid: 2f634fba-8dfa-4c7a-a8b9-be867b78d16a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f962306462538717df694d3bc47719fe31b1e1fe
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "76111475"
---
# <a name="configure-scenario-start-delays-in-load-tests"></a>配置负载测试中的方案启动延迟

使用负载测试编辑器和“属性”窗口先指定一个延迟，然后再在负载测试中启动某个方案  。

例如，如果需要一个方案开始生成另一个方案所使用的项，则可能希望使用“延迟开始时间”属性  。 可延迟该要使用生成项的方案以使生成项的方案能填充某些数据。

再如，可能有一个方案只在当天的某个特定时间运行。 因此，您希望延迟该方案的开始时间以对此进行模拟。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="specify-the-delay-start-time-of-a-scenario"></a>指定方案的延迟开始时间

通过使用负载测试编辑器在“属性”窗口中更改“延迟开始时间”属性，可以指定负载测试中某一方案开始前的延迟时间   。

> [!NOTE]
> 有关负载测试方案属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

例如，如果需要一个方案开始生成另一个方案所使用的项，则可能希望使用“延迟开始时间”属性  。 可延迟该要使用生成项的方案以使生成项的方案能填充某些数据。

再如，可能有一个方案只在当天的某个特定时间运行。 因此，您希望延迟该方案的开始时间以对此进行模拟。

> [!NOTE]
> 有关运行设置属性及其说明的完整列表，请参阅[负载测试方案属性](../test/load-test-scenario-properties.md)。

### <a name="to-specify-the-delay-start-time-for-a-scenario"></a>为方案指定延迟开始时间

1. 打开一个负载测试。

     此时将显示负载测试编辑器。 其中显示负载测试树。

2. 在负载测试树的“方案”文件夹中，选择要为其指定延迟开始时间的方案节点  。

3. 在“视图”菜单上选择“属性”窗口。  

     该方案的类别和属性将显示在“属性”窗口中  。

4. 在“延迟开始时间”属性文本框中，键入一个时间值，该时间值指示运行负载测试时，在负载测试开始之后而该方案开始之前等待的时间  。

    > [!NOTE]
    > 如果方案的“预热过程中禁用”属性值设置为“True”，则在预热期结束后将应用“延迟开始时间”属性时间值    。 使用“预热过程中禁用”方案属性可控制在预热中包含哪些方案  。

5. 更改属性后，在“文件”菜单上选择“保存”。   然后，可使用新的“延迟开始时间”值运行负载测试  。

## <a name="enable-and-disable-whether-a-scenario-runs-during-the-warm-up-period"></a>启用和禁用是否在预热期内运行方案

“预热过程中禁用”属性使用“属性”窗口设置   。 编辑负载测试方案属性通过负载测试编辑器进行设置。

“预热过程中禁用”属性用于指示在“延迟开始时间”属性指定的预热期内是否应运行方案   。 有关详细信息，请参阅上一个过程[指定方案的延迟开始时间](#specify-the-delay-start-time-of-a-scenario)。

> [!NOTE]
> 有关运行设置属性及其说明的完整列表，请参阅[负载测试运行设置属性](../test/load-test-scenario-properties.md)。

### <a name="to-enable-or-disable-the-warm-up-period-for-a-scenario"></a>启用或禁用方案的预热期

1. 打开一个负载测试。

     此时将显示“负载测试编辑器”  。 其中显示负载测试树。

2. 在负载测试树的“方案”  文件夹中，选择要为其更改启动行为的方案节点。

3. 在“视图”菜单上选择“属性”窗口。  

     该方案的类别和属性将显示在“属性”  窗口中。

     在“预热过程中禁用”属性中，选择“True”或“False”    。

4. 更改完此属性后，请选择“文件”菜单上的“保存”。   然后即可使用新的“预热过程中禁用”值运行负载测试  。

## <a name="see-also"></a>另请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [为负载测试配置测试代理和测试控制器](../test/configure-test-agents-and-controllers-for-load-tests.md)
- [负载测试方案属性](../test/load-test-scenario-properties.md)
