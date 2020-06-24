---
title: 添加用于负载测试的自定义计数器集
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- counters, counter sets
- counter sets
- load tests, counter sets
ms.assetid: 499aca80-1069-408d-ac68-326da6a50645
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e2b78cb68f1e7a7e1f47c6cc3e771353d7e46ca9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288424"
---
# <a name="how-to-add-custom-counter-sets-using-the-load-test-editor"></a>如何：使用负载测试编辑器添加自定义计数器集

在使用“新建负载测试向导”创建负载测试时，需添加一个初始计数器集  。 该计数器集为您的负载测试提供了一组预定义计数器集。

> [!NOTE]
> 如果负载测试分布在多台远程计算机之间，则会将控制器和代理计数器映射到控制器和代理计数器集中。 有关如何在负载测试中使用远程计算机的详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

在“负载测试编辑器”中管理计数器  。 已添加到测试中的计数器集会出现在负载测试的“计数器集”节点中。  创建负载测试之后，可以向其中添加新的自定义计数器集。

![自定义计数器集](../test/media/loadtestcustomcounter.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-a-custom-counter-set-to-a-load-test"></a>向负载测试添加自定义计数器集

1. 打开一个负载测试。

2. 展开“计数器集”节点。  添加到负载测试中的所有计数器集都会显示出来。

3. 右键单击“计数器集”节点，并选择“添加自定义计数器集”。  

    > [!NOTE]
    > 会向此计数器集赋予一个默认名称，如 Custom1  。 可以使用“属性”窗口更改该名称。  按 F4  以显示“属性”  窗口。

4. 若要向自定义计数器集添加计数器，请右键单击新的计数器集，然后选择“添加计数器”。  有关如何添加计数器的详细信息，请参阅[如何：向计数器集添加计数器](../test/how-to-add-counters-to-counter-sets-using-the-load-test-editor.md)。

    > [!NOTE]
    > 还可以通过右键单击现有计数器集，选择“复制”，然后将其粘贴到“计数器集”节点来添加自定义计数器集。 可以删除那些复制了但不需要的多余计数器。 可以使用“属性”窗口更改新计数器集的名称。 

## <a name="see-also"></a>另请参阅

- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
