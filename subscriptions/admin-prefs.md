---
title: 在管理门户中设置协议首选项
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 0fe9eaa4-f589-429e-a443-13bf86637d5a
ms.date: 03/17/2020
ms.topic: conceptual
description: 了解如何在管理门户中设置语言、联系人、订阅级别等的首选项
ms.openlocfilehash: e34b9cf1ed32abc81b9c2ebb3ef7c370818c9089
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87234609"
---
# <a name="set-preferences-for-your-agreements-in-the-administration-portal"></a>在管理门户中设置协议的首选项
超级管理员可以在管理门户中设置某些首选项，这些首选项将全局应用于每个协议。  这些首选项将在管理员添加订阅者时为管理员自动填充订阅详细信息，并且只能由超级管理员进行全局修改。  

## <a name="access-preferences"></a>访问首选项
必须使用在协议上具有超级管理员权限的登录 ID 登录[管理门户](https://manage.visualstudio.com)才能查看或修改首选项。  

设置首选项：
1. 请使用具有超级管理员权限的 ID 登录管理门户。
2. 单击“管理管理员”选项卡。
   > [!div class="mx-imgBorder"]
   > ![“管理员首选项”按钮](_img/admin-prefs/admin-prefs-button.png "依次单击“管理管理员”和“协议首选项”以显示首选项")

3. 单击“协议首选项”。
右侧将打开一个面板，显示可用的首选项。 

   > [!div class="mx-imgBorder"]
   > ![管理员首选项浮出控件对话框](_img/admin-prefs/admin-prefs-flyout.png "设置首选项，然后单击“保存”")

## <a name="set-your-preferences"></a>设置首选项
下面介绍每个可用的首选项及其效果。 

### <a name="agreement"></a>协议
如果你有多个超级管理员协议，则可以在下拉列表中选择所需的协议。  你设置的首选项仅适用于该协议。  在分配订阅时，各个管理员可以根据具体情况覆盖其中一些首选项。 

如果只有一个与你用于登录的电子邮件地址相关联的协议，则会显示该协议，并且将禁用下拉列表。 

### <a name="contact-email-address"></a>联系人电子邮件地址
此首选项提供了一种方法，可让订阅者通过使用订阅者门户的[订阅页面](https://my.visualstudio.com/subscriptions)上的“联系我的管理员”按钮与管理员联系。  如果此首选项留空，则订阅者消息将转发给协议上的所有管理员和超级管理员。  建议使用组电子邮件别名或安全组来定制此联系人电子邮件的受众群体。 如果你愿意，也可以选择输入个人的电子邮件地址。

> [!NOTE]
> 你在此处列出的电子邮件地址不会提供给订阅者。  当订阅者在订阅者门户中提交“联系我的管理员”请求时，消息将被转发到别名，而不会向订阅者公开。 

### <a name="default-external-subscribers-setting"></a>默认外部订阅者设置
借助此首选项可决定管理员是否可以从组织的租户/目录之外添加订户。  如果关闭此功能，则不允许任何外部订阅者。  如果启用该功能并且管理员尝试添加外部订阅者，则会要求他们确认他们的选择，并且将允许他们分配订阅。 管理员无法覆盖此设置。 

### <a name="default-downloads-setting"></a>默认下载设置
启用此设置（默认情况下处于启用状态）将使订阅者能够在管理员创建新订阅时访问下载。  管理员仍可基于单个订阅禁用下载。  如果禁用对下载的访问权限，则还会禁用对产品密钥的访问权限。  

### <a name="default-subscription-level"></a>默认订阅级别
可使用此设置确定在将订阅分配给用户时默认选择协议中包含的订阅级别。  管理员可以将设置更改为你协议中的任何订阅级别，这样便可避免重复做出最常见的选择。 

### <a name="default-communication-preferences"></a>默认通信偏好
设置默认通信语言和区域设置可以简化分配订阅的过程。  例如，如果你的开发团队位于与管理团队不同的国家/地区，则可以设置最适合订阅者位置的首选项。 对于单个订阅者，所有管理员仍然可以更改这些设置。 

## <a name="frequently-asked-questions"></a>常见问题
### <a name="q--can-i-disable-the-contact-email-address-so-subscribers-cannot-contact-administrators"></a>问：是否可以禁用“联系人电子邮件地址”，让订阅者无法联系到管理员？
答：否 - 虽然你可以使用安全组、组电子邮件别名或单个电子邮件地址来确定与哪些管理员联系，但不能禁用此功能。

### <a name="q-if-i-answer-a-subscribers-email-will-they-have-my-email-address"></a>问：如果我回复订阅者的电子邮件，他们会知道我的电子邮件地址么？
答：由于你的回复将来自你正在使用的任何电子邮件客户端，因此订阅者收到的回复将显示你正在使用的任何电子邮件地址。  因此，如果你从组别名进行回复，他们将看到组别名。  如果你使用自己的电子邮件地址回复，他们会看到该地址。  

### <a name="q-where-can-i-find-out-more-about-the-contact-my-admin-feature-in-the-subscriber-portal"></a>问：在哪里可以找到有关订阅者门户中“联系我的管理员”功能的详细信息？
答：请查看我们的[联系我的管理员](contact-my-admin.md)文章。 

### <a name="q-if-we-dont-complete-the-contact-email-address-and-a-subscriber-uses-the-contact-my-admin-feature-who-receives-their-request"></a>问：如果我们未完成“联系人电子邮件地址”，并且订阅者使用“联系我的管理员”功能，谁会收到他们的请求 ？
答：如果在“联系人电子邮件地址”首选项中没有设置特定的电子邮件地址，协议上的所有管理员都将收到请求。 

## <a name="resources"></a>资源
- [Visual Studio 管理和订阅支持](https://visualstudio.microsoft.com/support/support-overview-vs)

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
了解有关管理 Visual Studio 订阅的详细信息。
- [分配单个订阅](assign-license.md)
- [分配多个订阅](assign-license-bulk.md)
- [编辑订阅](edit-license.md)
- [确定最大使用量](maximum-usage.md)
