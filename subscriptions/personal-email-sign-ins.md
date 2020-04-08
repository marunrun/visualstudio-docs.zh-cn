---
title: VLSC 中显示的个人电子邮件
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 3f4b0528-03f0-4a02-b3c3-a39292a9bbe1
ms.date: 04/07/2020
ms.topic: conceptual
description: Visual Studio 订阅 – 为什么我会在我的订阅者中看到 Hotmail 或 Gmail 地址？
ms.openlocfilehash: e926caa8aef5a655b1f09ab8d6dbab1d70946827
ms.sourcegitcommit: 1f7aed335c48215dff5c151f76f22e3f10e8b564
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808340"
---
# <a name="visual-studio-subscriptions--why-do-i-see-personal-accounts-for-my-subscribers"></a>Visual Studio 订阅 - 我为什么会看到我的订阅者的个人帐户？
随着公司从批量许可服务中心 (VLSC) 迁移到新的 Visual Studio [订阅管理门户](https://manage.visualstudio.com)，管理员惊奇地发现某些订阅者的“登录电子邮件地址”显示 Hotmail 或 Outlook 等个人电子邮件地址。  有关详细信息，请观看[此视频](https://www.youtube.com/watch?v=J61EYaVN-dQ&list=PLReL099Y5nReJhZ6o8CQFPSBgzGCHX99_&index=6)。

## <a name="cause"></a>原因
由于登录进程与旧版 MSDN 订阅者体验相关联，因此会出现这种情况。 用户在没有修改的情况下从批量许可服务中心 (VLSC) 迁移到了 Visual Studio 订阅管理门户。 管理员可能没有意识到，用户一直在使用个人帐户来访问他们的订阅权益。 在 Visual Studio 订阅者迁移之前（已于 2016 年完成迁移），要成功使用 Visual Studio 订阅需执行以下两个操作：
1. 管理员通过订阅者的工作或学校电子邮件地址，将订阅“分配”给每个订阅者。
2. 订阅者“激活”订阅。

在订阅者激活期间：需要使用 Microsoft 帐户 (MSA) 登录。 如果订阅者未尝试使其工作或学校帐户（例如tasha@contoso.com）成为 MSA，他们可以创建一个新的 MSA，或利用现有 MSA。 这将导致他们的“登录电子邮件地址”不同于其“分配到的电子邮件地址”。

> [!NOTE]
> [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 上的新式订阅者体验同时支持工作/学校标识类型和 Microsoft 帐户 (MSA) 标识类型。

## <a name="solution"></a>解决方案

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4th6B]

要解决此问题，只需选择“连接电子邮件”按钮，然后系统会尝试根据匹配姓氏和名字，将具有 MSA 的帐户与你组织的 Azure Active Directory (Azure AD) 中的现有用户相匹配。 如果出现错误，你可单击任何匹配项右侧的 X，删除该匹配项。  

> [!div class="mx-imgBorder"]
> ![“连接电子邮件”按钮](_img/connect-emails/connect-emails-button.png)

你还可使用“搜索目录”来更正问题或填入来自 Azure AD 的缺失信息。 如果所有匹配看起来都正确，你可选中“选择所有匹配的订阅者”，而不是一次选择一人。  

> [!div class="mx-imgBorder"]
> ![“连接电子邮件”弹出式菜单](_img/connect-emails/connect-emails-flyout.png)

接下来单击“继续”，这将转到一个屏幕，上面概要列出了要进行的更改。 如果同意，请单击“保存”，然后就会进行更改。 你的订阅者还将在下次登录自己的订阅时收到一条消息，其中显示所进行了更改。   

> [!div class="mx-imgBorder"]
> ![“连接电子邮件”确认](_img/connect-emails/connect-emails-confirm.png) 

> [!NOTE]
> 编辑登录电子邮件地址时，这只会更新订阅者用于在 https://my.visualstudio.com 上登录其订阅的电子邮件地址。 如果订阅者已使用其他电子邮件地址激活 Azure 或 Pluralsight 等权益，则他们需要继续使用这些地址才能使用这些权益。 对于他们获得的任何新权益，他们应使用新的电子邮件地址。 

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

##  <a name="next-steps"></a>后续步骤
- 一旦更新订阅者电子邮件地址，你需要通知他们其登录信息已更改。  他们还将收到一封包含更新信息的电子邮件。
- [筛选组织中的订阅者列表](search-license.md)以查找可能需要更改的任何登录电子邮件地址可能会很有用。  
