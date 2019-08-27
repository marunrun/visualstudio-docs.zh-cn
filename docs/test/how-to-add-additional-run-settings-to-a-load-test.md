---
title: 向负载测试添加运行设置
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, run settings, adding
- load tests, run settings
ms.assetid: 257d2a24-d582-4cfe-8b2b-51f51ba9cc84
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c1d7f9d0c9ad07223d0b59d7aeca585b53432280
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63002239"
---
# <a name="how-to-add-additional-run-settings-to-a-load-test"></a>如何：向负载测试添加额外的运行设置

负载测试的运行设置将确定各种其他设置， 包括测试持续时间、结果集详细程度以及测试运行时收集的计数器集。 可以为每个负载测试创建和存储多个运行设置，然后在运行测试时选择一个要使用的特定设置。 使用“新建负载测试向导”创建负载测试时，将向负载测试添加初始运行设置。

可以向具有不同属性设置的负载测试中添加更多的运行设置，以便能够在不同条件下运行负载测试。 例如，可以添加新测试设置，并使用一个不同的采样率，或指定一个较长的运行持续时间。 一次只能使用一个运行设置，并且必须通过将要使用的运行设置标记为活动来指定该运行设置。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-another-run-setting"></a>添加另一个运行设置

1. 打开一个负载测试。

2. （可选）展开“运行设置”文件夹。

3. 右键单击“运行设置”文件夹并选择“添加运行设置”。

     将一个新的运行设置添加到“运行设置”文件夹中。

4. 在“视图”菜单上，选择“属性”窗口。

     此时将显示“属性”窗口，其中包含了所选运行设置的属性。

5. 在“属性”窗口中，使用“名称”属性文本框为新运行设置指定一个名称，该名称描述此运行设置的目的（例如“Run Setting: Five minute run”）。

6. 使用“属性窗口”更改运行设置。 例如，将运行持续时间更改为“00:05:00”以使测试运行五分钟。

    > [!NOTE]
    > 有关运行设置属性及其说明的完整列表，请参阅[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。

     现在可以通过以下方式指定您希望使用已添加的运行设置：将其设置为“活动”。 有关详细信息，请参阅[如何：为负载测试选择活动运行设置](../test/how-to-select-the-active-run-setting-for-a-load-test.md)。

## <a name="see-also"></a>请参阅

- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)