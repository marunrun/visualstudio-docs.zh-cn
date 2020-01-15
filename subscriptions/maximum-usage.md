---
title: 在管理门户中使用最大用量功能
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/24/2019
ms.topic: conceptual
description: 了解如何在管理门户中查看分配的最大订阅数
ms.openlocfilehash: 76360c9843d82350a2b9929b8debfdb4aa4cde82
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852331"
---
# <a name="use-the-maximum-usage-feature-to-track-the-number-of-assigned-subscriptions"></a>使用最大用量功能跟踪分配的订阅数
Visual Studio 订阅管理门户中的新功能有助于跟踪已购买和分配的订阅数量，并确定在过去一年和整个协议期间分配的每个级别的峰值订阅数。 

## <a name="view-your-maximum-usage"></a>查看最大用量
查看为任何协议和订阅级别分配的峰值订阅数：
1. 在门户左上角的下拉列表中选择要查看的协议。 （若只有一个协议，则已经选择了该协议。）
2. 单击“最大用量”选项卡  。  
    > [!div class="mx-imgBorder"]
    > ![最大用量菜单](_img/maximum-usage/maximum-usage-menu.png)
3. 随即显示“最大用量摘要”、过去一年为各个级别分配的最大订阅数以及达到该峰值的日期。  如果多次达到该峰值，则显示第一次达到该峰值的日期。 
    > [!div class="mx-imgBorder"]
    > ![最大用量摘要](_img/maximum-usage/maximum-usage-summary.png)
4. 要查看在协议有效期内分配的最大订阅数，请单击“完整期限”选项卡  。

## <a name="view-your-assignment-history"></a>查看分配历史记录
除了查看各个订阅级别的峰值分配外，还可以单击“导出完整报表”按钮，查看协议上活动的运行帐户，包括购买和分配  。  

> [!div class="mx-imgBorder"]
> ![最大用量完整报表](_img/maximum-usage/maximum-usage-full-report.png)

对于每个订阅级别，该报表会显示达到新的最大分配级别的日期以及截至该日期购买的订阅数，可用于轻松查看任何超额分配的日期。  

例如，在上表中可以看到，2018 年 12 月 13 日协议中有 123 个 Visual Studio Enterprise 订阅，并且分配了 120 个订阅。  2019 年 1 月 8 日，又分配了一个订阅，使分配总数达到了 121。  第二天，又分配了六个订阅，并在协议中添加了四个订阅，以涵盖新的分配。  

## <a name="frequently-asked-questions"></a>常见问题
### <a name="q-how-is-the-information-in-the-maximum-usage-different-from-the-assignment-information-available-in-the-overview-section-on-the-left-side-of-the-portal"></a>问：最大用量中的信息与门户左侧“概述”部分中提供的分配信息有何不同？
答：概述中的信息显示每个订阅级别的当前分配和可用订阅  。  这可能与在当前年度或协议有效期内为协议分配的最大订阅数有很大不同。  使用最大用量功能，可查看达到最大分配级别的时间及达到的具体级别。  这是一个重要的区别，因为在校准期间是根据全年任何时候分配的最大订阅数对订阅进行计费的。 

## <a name="resources"></a>资源
- [Visual Studio 授权白皮书](https://visualstudio.microsoft.com/wp-content/uploads/2019/06/Visual-Studio-Licensing-Whitepaper-May-2019.pdf)
- [Visual Studio 管理和订阅支持](https://visualstudio.microsoft.com/support/support-overview-vs)
- [批量许可条款](https://www.microsoft.com/licensing/product-licensing/products.aspx)

## <a name="next-steps"></a>后续步骤
- 如果对订阅分配或门户管理的其他方面有任何疑问，请联系 https://visualstudio.microsoft.com/subscriptions/support/ 获取帮助。 
- 详细了解如果分配的订阅数超过了所购买的订阅数（称为[超额分配](handle-overclaimed-license.md)）应该怎么办。
