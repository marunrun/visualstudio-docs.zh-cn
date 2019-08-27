---
title: 处理超额分配的许可证 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/24/2019
ms.topic: conceptual
description: 了解管理员如何解决超额分配的订阅
ms.openlocfilehash: 924f6fb2c513d70aefd28c1d4ff18d1af62178c2
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605506"
---
# <a name="overallocated-subscriptions"></a>过度分配的订阅
有时，添加订阅者后，订单发生变化，这可能会导致已分配的订阅数量超过公司拥有的许可证数量。 这称为“超额分配”。  发生这种情况时，“订阅者”选项卡会显示警报，并为你提供有关超额分配了多少订阅的详细信息。

> [!NOTE]
> 开放式许可证计划不允许出现超额分配。  另外，其他程序可能会在门户中以不同方式显示此信息。
>
> [!div class="mx-imgBorder"]
> ![透支订阅通知](_img/over-claimed/over-claimed-alert.png)

## <a name="resolve-overallocated-subscriptions"></a>解决超额分配的订阅
有多种方法可解决超额分配：
- 请与经销商联系以购买其他订阅。
- 等到你的年度校正期并在此时为超额分配的订阅付款。 
- 删除某些订阅分配。  （这仍需要在年度校正期付款，因为校正基于一年中任何时间分配的最大订阅数。）

## <a name="billing-and-true-up"></a>计费和校正
如果你的组织具有企业协议 (EA)，则管理员无需购买订阅即可分配它们，稍后再通过被称作“校正”的对帐过程支付相关费用。  如果过度分配，则在“校正”期间，将按分配给用户的最大订阅数向你的组织计费。  即使在校正发生期间你分配的订阅数不再达到上限，也是如此。  要详细了解如何监视你的最大用量，请访问[最大用量](maximum-usage.md)主题。

> [!Important]
> 如果 Visual Studio 订阅管理员分配了带有 GitHub Enterprise 的 Visual Studio 订阅，且从未购买过这些订阅，则它们将对组织中的 GitHub Enterprise 管理员不可见。 要确保 GitHub Enterprise 订阅可见，应在首次分配订阅时至少购买一个带 GitHub Enterprise 的 Visual Studio Professional 订阅或带 GitHub Enterprise 的 Visual Studio Enterprise 订阅  。
>
> 由客户负责确保在管理门户中针对所分配的每个 GitHub 订阅都分配了一个对应的带 GitHub 的 Visual Studio 订阅，从而保证符合此订阅的许可要求。

## <a name="next-steps"></a>后续步骤
- 详细了解如何管理[带有 GitHub Enterprise 的 Visual Studio 订阅](assign-github.md)。
- 有关 Visual Studio 订阅的销售、订阅、帐户和账单的帮助，请与 Visual Studio [订阅支持](https://visualstudio.microsoft.com/subscriptions/support/)联系。
