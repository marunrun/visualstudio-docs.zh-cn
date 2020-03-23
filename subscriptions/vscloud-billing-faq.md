---
title: Visual Studio Enterprise 和 Visual Studio Professional 云订阅计费常见问题解答
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/28/2019
ms.topic: conceptual
description: 云订阅的计费问题。
ms.openlocfilehash: c4544df196d3e861522dfcbb877a90a5656ad7ba
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "75851410"
---
# <a name="visual-studio-cloud-subscriptions-billing-faq"></a>Visual Studio 云订阅计费常见问题解答
请确保[比较云订阅权益和定价](https://visualstudio.microsoft.com/vs/pricing/)，了解每种 Visual Studio 订阅的权益，云订阅与标准 Visual Studio 订阅之间的不同之处，以及订阅者权益的相关详细信息等。

## <a name="general-purchasing-questions"></a>购买的常见问题
### <a name="q-can-i-buy-visual-studio-cloud-subscriptions-using-a-purchase-order"></a>问：我可以使用采购订单购买 Visual Studio 云订阅吗？
答：不是。 所有 Visual Studio 云订阅都必须使用 Azure 订阅购买。 （可将其视作你的 Azure 计费帐户。）

### <a name="q-what-types-of-azure-subscriptions-can-be-used-to-buy-visual-studio-cloud-subscriptions"></a>问：哪些类型的 Azure 订阅可用于购买 Visual Studio 云订阅？
答：可使用大多数 Azure 订阅 - 我们支持连接到[企业协议 (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/) 的 Azure 订阅、由云解决方案提供商 (CSP) 设置的 Azure 订阅、通过 Microsoft Open License 经销商设置的 Azure 订阅和即用即付 Azure 订阅。

无法使用某些类型的 Azure 订阅，包括 [Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/)和作为订阅者权益包含在 Visual Studio 订阅中的订阅。

### <a name="q-am-i-required-to-buy-other-azure-services"></a>问：我是否需要购买其他 Azure 服务？
答：完全不需要。 通过 Azure，可以仅购买 Visual Studio 云订阅。

## <a name="enterprise-agreement-ea-customers"></a>企业协议 (EA) 客户
### <a name="q-can-i-use-an-enterprise-agreement-to-buy-visual-studio-cloud-subscriptions"></a>问：我可以使用企业协议购买 Visual Studio 云订阅吗？
答：可以。 你需要是为你的 EA 创建的 Azure 订阅的所有者或参与者。 请确保直接在 Visual Studio Marketplace 中购买 Visual Studio 云订阅。 不能使用采购订单购买 Visual Studio 云订阅。

### <a name="q-how-can-i-tell-whether-i-have-the-necessary-privileges-to-buy-services-in-the-visual-studio-marketplace-through-my-organizations-enterprise-agreement"></a>问：如何通过组织的企业协议判断是否具有在 Visual Studio Marketplace 中购买服务所需的权限？
答：确定是否拥有正确权限的最简单方法是单击“购买”按钮，查看 Visual Studio Marketplace 中提供的服务  。
需要从出现的当前链接到登录名的 Azure 订阅列表中选择一个 Azure 订阅（即计费帐户）。
由于 Azure 订阅的名称默认为计费帐户的类型（“即用即付”、“企业协议”等），因此通常很容易判断 Azure 订阅是否为企业协议的一部分。

另一种方法是尝试访问 [Azure 企业门户](https://ea.azure.com)。  如果可以成功访问，说明已经具有企业管理员或帐户所有者角色。 只有帐户所有者才能在企业协议中设置新的 Azure 计费帐户。 如果无法访问 Azure 企业门户，请咨询你的组织并联系企业管理员将你添加为 Azure 企业门户中的帐户所有者。  如果联系不到管理员，可以[提交支持票证](https://support.microsoft.com/supportrequestform/cf791efa-485b-95a3-6fad-3daf9cd4027c)并请求联系信息。  需要提供组织名称以及支持票证的企业协议注册号。

### <a name="q-can-i-use-the-azure-monetary-commitment-funds-from-my-enterprise-agreement-to-buy-visual-studio-cloud-subscriptions"></a>问：我可以使用来自企业协议的 Azure 货币承诺资金购买 Visual Studio 云订阅吗？
答：不可以，这些预付资金不具备购买 Visual Studio 云订阅的资格。 当选择为 EA 创建的 Azure 订阅来购买 Visual Studio 云订阅时，这些费用会显示在下一张“超额”发票上。 通常该情况每月都会发生，但由于某些 EA 客户的历史规则，可能在几个月内不会开具超额发票。 如需了解额外购买量（不符合 Azure 货币承诺资金的购买量）是否会触发超额发票，请咨询 EA 的许可专家。

## <a name="how-charges-are-processed"></a>如何收费
### <a name="q-how-are-monthly-cloud-subscription-charges-processed"></a>问：“月度”云订阅是如何收费的  ？
答：在第一次购买时，我们会根据当月的剩余天数按比例收费。 例如，如果在 4 月 15 日购买了 10 个 Visual Studio Professional 月度云订阅，则只收取 5 个单位的费用，因为该月剩余 50% 的天数（30 天月份中的 15 天）。
在 5 月的第一天以及此后的每个月，对全部 10 个单位收费，直到取消。

当在之后增加付款订阅数量时，我们同样会根据当月的剩余天数按比例对新增单位计费。 因此，如果在 5 月 10 日再购买 1 个 Visual Studio Professional 月度云订阅，则收取大约 0.677 个单位（距离 5 月 31 日还剩余 21 天）的费用。

### <a name="q-how-are-annual-cloud-subscription-charges-processed"></a>问：“年度”云订阅是如何收费的  ？
答：在每次购买时，都会即时对已购买的全部数量计费。 费用不会按该年的剩余天数收取，也不会按比例分配。 如果在一年中的不同时间购买年度云订阅，则订阅的续订月份也不同。 与 Microsoft 批量许可协议采购一样，我们并未将所有客户的年度云订阅都视为有共同的时间边界。

### <a name="q-how-do-cancelations-work"></a>问：取消如何工作？
答：当取消 Visual Studio 云订阅时，会同时取消自动续订。 订阅会一直持续到正常的续订日期，并于该日期后直接过期。
到期后，Visual Studio 订阅者无法继续使用 Visual Studio 或订阅中的任何其他权益。

对于月度云订阅，取消在次月第一天生效。 如果只取消部分月度云订阅，请务必在次月的第一天删除用户，确保为正确的人员继续分配活动订阅。

对于年度云订阅，取消在最初购买日 12 个月后的次月第一天生效，或在上一次年度续订收费后的 12 个月后生效。 例如，如果在 2018 年 1 月 3 日购买了 Visual Studio Professional 年度云订阅，那么它会保持活动状态，直到 2019 年 2 月 1 日自动续订一年。 如果在 2020 年 2 月 1 日之前的任何时间取消订阅，则订阅于 2020 年 2 月 1 日到期。 对于年度云订阅取消后的剩余部分，不会进行退款。

### <a name="q-what-kind-of-volume-discounts-are-available-for-visual-studio-subscriptions"></a>问：Visual Studio 订阅支持哪些类型的批量折扣？
答：“每种“订阅的第 6 个订阅及所有后续订阅可享受 5% 的折扣  ：

* Visual Studio Professional 月度
* Visual Studio Professional 年度
* Visual Studio Enterprise 月度
* Visual Studio Enterprise 年度

例如，如果购买了 6 个 Visual Studio Professional 月度订阅和 5 个 Visual Studio Enterprise 月度订阅，则需支付 5 个 Professional 订阅的正常价格，第 6 个 Professional 订阅可享受 5% 的折扣，但所有 5 个 Enterprise 订阅将按正常价格收费。

此外，折扣仅适用于给定月度计费周期内的费用。 因此，如果在一个月内购买了 5 个 Visual Studio Professional 年度订阅，然后在次月再次购买了 5 个，则需按正常价格支付所有 10 个订阅的费用。

> [!NOTE]
> Microsoft 不再在云订阅中提供 Visual Studio Professional 年度订阅和 Visual Studio Enterprise 年度订阅。 现有客户体验以及续订、增加、减少或取消订阅的能力不会发生变化。 建议新客户访问 [https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/)，查看各 Visual Studio 购买选项。

## <a name="other-questions"></a>其他问题
### <a name="q-can-i-use-the-monthly-azure-devtest-individual-credit-as-a-visual-studio-subscriber-to-buy-more-visual-studio-cloud-subscriptions"></a>问：我可否以 Visual Studio 订阅者的身份，使用每月 Azure 开发测试个人额度购买更多 Visual Studio 云订阅？
答：不可以，不能以 Visual Studio 订阅者的身份使用[每月 Azure 开发测试额度](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)在 Visual Studio Marketplace 中购买产品。 任何 Visual Studio 云订阅购买都会对信用卡计费。
购买之前，需要先[移除支出限制](https://azure.microsoft.com/pricing/spending-limits/)。

### <a name="q-whats-the-difference-between-annual-and-monthly-cloud-subscriptions"></a>问：年度和月度云订阅有何区别？
答：月度云订阅包括 Visual Studio 以及 Azure DevOps Services 和 TFS 的使用权。 年度云订阅除具备上述权益外，还提供订阅者权益，其中包括使用 Windows 和其他 Microsoft 软件安装和运行以进行开发和测试、将每月 Azure 开发测试个人额度用于试用 Azure 服务以及在云中进行开发和测试、培训和支持等等。
[比较云订阅权益和定价](https://visualstudio.microsoft.com/vs/pricing/)

### <a name="q-do-i-get-new-versions-of-visual-studio-if-i-buy-a-visual-studio-cloud-subscription"></a>问：如果我购买 Visual Studio 云订阅，是否会获得 Visual Studio 的新版本？
答：可以。 新版本发布后，你可以下载并运行。 同时也可以继续运行以前的版本。

### <a name="q-can-i-buy-visual-studio-cloud-subscriptions-from-my-software-reseller"></a>问：我可以从软件经销商处购买 Visual Studio 云订阅吗？
答：可以，但前提是该经销商参与了云解决方案提供商 (CSP) 计划。 请向其进行咨询。

## <a name="related-resources"></a>相关资源
- [Visual Studio 订阅管理门户](https://manage.visualstudio.com/)
- [Visual Studio 订阅支持](https://visualstudio.microsoft.com/vs/support/)
- [适用于 CSP 的 Visual Studio 云订阅购买](vscloud-csp.md)

## <a name="next-steps"></a>后续步骤
立即购买云订阅
- [Visual Studio Professional 月度](https://marketplace.visualstudio.com/items?itemName=ms.vs-professional-monthly)
- [Visual Studio Enterprise 月度](https://marketplace.visualstudio.com/items?itemName=ms.vs-enterprise-monthly)
