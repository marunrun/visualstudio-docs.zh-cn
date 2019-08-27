---
title: 适用于 CSP 的 Visual Studio 云订阅购买
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/28/2019
ms.topic: conceptual
description: 有关云解决方案提供商如何为客户购买和管理 Visual Studio 云订阅的信息。
ms.openlocfilehash: 7711d9296ca26a09f251f70a6f8dc4848f769507
ms.sourcegitcommit: a124076dfd6b4e5aecda4d01984fee7b0c034745
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68787750"
---
# <a name="buy-and-manage-visual-studio-cloud-subscriptions-for-your-customers"></a>为客户购买和管理 Visual Studio 云订阅
[云解决方案提供商 (CSP)](https://partner.microsoft.com/cloud-solution-provider) 计划中的合作伙伴可为其客户购买 Visual Studio Enterprise 和 Visual Studio Professional 云订阅。

[比较云订阅选项](https://visualstudio.microsoft.com/vs/pricing)

> [!NOTE]
> Microsoft 不再在云订阅中提供 Visual Studio Professional 年度订阅和 Visual Studio Enterprise 年度订阅。 现有客户体验以及续订、增加、减少或取消订阅的能力不会发生变化。 建议新客户访问 [https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/)，查看各 Visual Studio 购买选项。

## <a name="prerequisites"></a>系统必备
必须先在合作伙伴中心设置客户租户，并为此租户创建 Azure 订阅。

[了解更多信息](/azure/devops/organizations/billing/csp/set-up-csp-customer)

## <a name="who-can-buy-visual-studio-subscriptions"></a>谁可以购买 Visual Studio 订阅？
拥有 Azure 订阅[所有者或参与者访问权限](https://na01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fvsts%2Forganizations%2Fbilling%2Fadd-backup-billing-managers%3Fview%3Dvsts%2520%2520sa&data=02%7C01%7C%7Cb9e717e8abff47b0cd7e08d618edd860%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636723807145220358&sdata=aIaamEXHhx94KCYVY%2FFibqFzNBEqKPntpql867xAMgU%3D&reserved=0)的任何人都可以购买 Visual Studio 订阅。

## <a name="how-to-buy"></a>购买方式

1. 登录 [Microsoft 合作伙伴中心](https://partnercenter.microsoft.com)。
0. 选择“客户”，并选择要为其购买的客户  。
0. 选择“服务管理”  。
0. 选择“Visual Studio Marketplace”  。
0. 确保客户名位于右上角。
0. 选择“订阅”  。
0. 选择“Visual Studio Enterprise”或“Visual Studio Professional”。
0. 选择“购买”  。
0. 选择用于为购买计费 Azure 订阅。
0. 输入客户所需的用户数量。
0. 查看订单并“确认”  。

>[!NOTE]
> 每次作为 CSP 购买 Visual Studio 订阅时，都需要执行这些步骤。 目前尚无自动完成采购的 API。

确认购买后，可以选择“管理”，将订阅分配给客户的最终用户  。  还可以通过选择“服务管理”，从合作伙伴中心访问订阅管理门户  。  在其中可看到以下步骤或视频。

## <a name="how-to-manage-visual-studio-cloud-subscriptions-for-your-customer"></a>如何为客户管理 Visual Studio 云订阅

1. 登录 [Microsoft 合作伙伴中心](https://partnercenter.microsoft.com)。
0. 选择“客户”和客户名  。
0. 选择“服务管理”  。
0. 选择“管理 Visual Studio 订阅”  。

如果此客户拥有多个 Azure 订阅，请使用下拉菜单选择从你这里购买的 Azure 订阅。  “许可证摘要”显示已分配的订阅数量以及每个 Visual Studio 云订阅选项可用的订阅数量  。  摘要还允许你购买更多订阅或减少订阅数量。

选择“添加”，向新用户分配订阅  。  显示的计数会更新，同时最终用户会收到电子邮件通知。 最终用户可以使用你提供的电子邮件地址登录，并在 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)中激活其 Visual Studio 订阅。

若要将 Visual Studio 订阅重新分配给其他用户，可以删除当前订阅者并添加新的订阅者。

如果用户尚未激活其 Visual Studio 订阅，可能是因为他们未收到邀请电子邮件。  你也可以从 Visual Studio 管理门户中请求我们向用户重新发送激活邀请。

## <a name="view-visual-studio-pricing-for-csp-partners"></a>查看适用于 CSP 合作伙伴的 Visual Studio 定价
若要查看适用于 CSP 合作伙伴的 Visual Studio 定价，请登录[合作伙伴中心](https://partnercenter.microsoft.com)。  从左侧导航栏中选择“定价和优惠”  。  选择右上方“基于使用情况的服务”下的当前月份定价文件  。 下载 Excel 电子表格后，转到“Azure 价目表”工作表，并在“计量类别”列筛选出“Visual Studio”    。

下面解释了在此电子表格中看到的内容：

| 计量类别    |   name                 |  单位                                |           这是什么                          |
|-------------------|------------------------|---------------------------------------|-------------------------------------------------|
| Visual Studio     | 企业             |  订阅                         | Visual Studio Enterprise 月度订阅   |
| Visual Studio     | Professional           |  订阅                         | Visual Studio Professional 月度订阅 |

我们为每月（为给定客户）购买的每种 Visual Studio 订阅的第 6 个单位提供 5% 的折扣。 因此，每个订阅会显示两行选项。 一行显示“最小值”为 0，应该将其理解为第 1 至 5 个单位的基准价格。 另一行显示“最小值”为 5，这是适用于第 6 个及以上单位的 5% 折扣价格。

## <a name="frequently-asked-questions"></a>常见问题
### <a name="q-how-are-monthly-cloud-subscription-charges-processed"></a>问：“月度”云订阅是如何收费的  ？
答：在第一次购买时，我们会根据当月的剩余天数按比例收费。 例如，如果在 4 月 15 日购买了 10 个 Visual Studio Professional 月度云订阅，则只收取 5 个单位的费用，因为 30 天月份还剩 15 天（或者说 50%），我们会按照 50% 的比例收费。 在 5 月的第一天以及此后的每个月，对全部 10 个单位收费，直到取消。

当在之后增加付款订阅数量时，我们同样会根据当月的剩余天数按比例对新增单位计费。 因此，如果在 5 月 10 日再购买 1 个 Visual Studio Professional 月度云订阅，则收取大约 0.677 个单位（距离 5 月 31 日还剩余 21 天）的费用。

### <a name="q-how-do-cancellations-work"></a>问：取消如何工作？
答：当取消 Visual Studio 云订阅时，会同时取消自动续订。 订阅会一直持续到正常的续订日期，并于该日期后直接过期。 到期后，Visual Studio 订阅者无法继续使用 Visual Studio 或订阅中的任何其他权益。

对于月度云订阅，取消在次月第一天生效。 如果只取消客户的部分月度云订阅，请务必在次月的第一天删除用户，确保为正确的人员继续分配活动订阅。

对于年度云订阅，取消在最初购买日 12 个月后的次月第一天生效，或在上一次年度续订收费后的 12 个月后生效。 例如，如果在 2018 年 1 月 3 日购买了 Visual Studio Enterprise 年度云订阅，那么它会保持活动状态，直到 2019 年 2 月 1 日自动续订一年。 如果在 2020 年 2 月 1 日之前的任何时间取消订阅，则订阅于 2020 年 2 月 1 日到期。 对于年度云订阅取消后的剩余部分，不会进行退款。

### <a name="q-what-kind-of-volume-discounts-are-available-for-visual-studio-subscriptions"></a>问：Visual Studio 订阅支持哪些类型的批量折扣？
答：“每种“订阅的第 6 个订阅及所有后续订阅可享受 5% 的折扣  ：
- Visual Studio Professional 月度
- Visual Studio Enterprise 月度

例如，如果购买了 6 个 Visual Studio Professional 月度订阅和 5 个 Visual Studio Enterprise 月度订阅，则需支付 5 个 Professional 订阅的正常价格，第 6 个 Professional 订阅可享受 5% 的折扣，但所有 5 个 Enterprise 订阅将按正常价格收费。

此外，折扣仅适用于给定月度计费周期内的费用。 因此，如果在一个月内购买了 5 个 Visual Studio Professional 年度订阅，然后在次月再次购买了 5 个，则需按正常价格支付所有 10 个订阅的费用。

这些折扣反映在[合作伙伴中心](https://partnercenter.microsoft.com)的定价数据中。

### <a name="q-are-there-renewal-discounts"></a>问：续订是否有折扣？
答：否，Visual Studio 订阅的价格是固定的。 新订阅和继续订阅的价格相同。

### <a name="q-are-there-azure-devtest-pricing-options-for-csps"></a>问：有适用于 CSP 的 Azure 开发/测试定价选项吗？
答：暂时没有。 客户可以使用 [Azure 开发/测试定价](https://aka.ms/azuredevtestpricing)，但目前没有专门适用于 CSP 的任何内容。

