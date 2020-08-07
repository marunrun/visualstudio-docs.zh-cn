---
title: 处理超额分配的许可证 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: a747100c-6f08-41a4-aaad-05099741742b
ms.date: 03/03/2020
ms.topic: conceptual
description: 了解管理员如何解决超额分配的订阅
ms.openlocfilehash: b518dc9300862e7c39af0489734734668097ef9f
ms.sourcegitcommit: b8ec700fc4c14c68c6ce280f29c19870261990d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87453727"
---
# <a name="over-allocated-subscriptions"></a>超额分配的订阅
有时，添加订阅者后，订单发生变化，这可能会导致已分配的订阅数量超过公司拥有的许可证数量。 这称为“超额分配”。  

要查看你的订阅分配情况，请单击左侧的顶部图标，打开分配窗格。  

> [!NOTE]
> 开放式许可证计划不允许出现超额分配。  另外，其他程序可能会在门户中以不同方式显示此信息。
>
> [!div class="mx-imgBorder"]
> ![透支订阅通知](_img/over-claimed/over-claimed-alert.png "“概述”中列出了超额分配的数量，由每个订阅类型的关系图上经过哈希处理的条形表示。")

请注意，显示项使用经过哈希处理的条形来表示超额分配的订阅。  所有订阅类型的超额分配数都包含在顶部的“概述”部分，而每个订阅级别还会显示它自己的分配状态。  

## <a name="resolve-over-allocated-subscriptions"></a>解决超额分配的订阅
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

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 详细了解如何管理[带有 GitHub Enterprise 的 Visual Studio 订阅](assign-github.md)。
- 有关 Visual Studio 订阅的销售、订阅、帐户和账单的帮助，请与 Visual Studio [订阅支持](https://visualstudio.microsoft.com/subscriptions/support/)联系。