---
title: 使用别名登录 Visual Studio 订阅可能会失败 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/19/2019
ms.topic: conceptual
description: 如果别名或友好名称已被使用，登录可能会失败
ms.openlocfilehash: 392b86699b1116f45ca75df3b611fff6a2aebc62
ms.sourcegitcommit: 485881e6ba872c7b28a7b17ceaede845e5bea4fe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2019
ms.locfileid: "68378020"
---
# <a name="signing-in-to-visual-studio-subscriptions-may-fail-when-using-aliases"></a>使用别名登录 Visual Studio 订阅可能会失败
根据用于登录的帐户类型，登录 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 时，可用订阅可能无法正确显示。 一个潜在的原因是使用了“别名”或“友好名称”来代替订阅所分配到的登录标识。 这就是所谓的“别名”。

## <a name="what-is-aliasing"></a>别名是什么？
“别名”一词是指具有不同身份的用户登录 Windows（或 Active Directory）并访问电子邮件。

当公司为其目录登录（例如“JohnD@contoso.com”）提供 Microsoft Online Service 时，可能会遇到别名，但用户使用别名或友好名称（例如“John.Doe@contoso.com”）访问其电子邮件帐户。 对于通过批量许可服务中心 (VLSC) 管理其订阅的许多客户来说，由于提供的电子邮件地址（“John.Doe@contoso.com”）与通过“工作或学校帐户”选项成功进行身份认证所需的目录地址（“JohnD@contoso.com”）不匹配，这种做法可能会导致登录失败。

## <a name="as-an-administrator-what-options-do-i-have"></a>作为管理员，有哪些选项可供我选择？
作为管理员，有两种选择可确保你的订阅者在 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 上成功登录。
- 第一个选项（建议）是将目录帐户作为批量许可服务中心 (VLSC) 中分配的地址。 有关详细信息，请参阅本文中[将订阅者分配给目录帐户](#assigning-subscribers-to-a-directory-account)部分。
- 第二种选项（较不安全）是允许订阅者将他们的“工作或学校”电子邮件地址与“个人”帐户（又名： Microsoft 帐户或 MSA）关联。 有关详细信息，请参阅本文[将工作或学校帐户定义为个人帐户](#defining-a-work-or-school-account-as-a-personal-account)部分。

> [!NOTE]
> 公司迁移到新的 Visual Studio 订阅[管理门户](https://manage.visualstudio.com)后，你将能够利用新的管理体验，可将目录和电子邮件地址作为订阅者个人资料的一部分提供。 详细了解此[迁移](https://support.microsoft.com/help/4013930/visual-studio-subscriptions-administrator-migration-details)。

## <a name="assigning-subscribers-to-a-directory-account"></a>将订阅者分配到目录帐户
在所有情况下，批量许可服务中心 (VLSC) 内的订阅管理器将需要使用新订阅者的目录地址，或更新“现有”订阅者的电子邮件地址。 请注意，使用目录地址将意味着所有新的订阅者都不会收到欢迎电子邮件，管理员将需要通知订阅者订阅已分配给他们。 按照以下步骤操作之后，还可以随时使用电子邮件[模板](#notifying-your-subscribers-with-directory-addresses)通知订阅者，并帮助他们完成登录过程。

### <a name="adding-new-subscribers"></a>添加新订阅者
请按照以下步骤通过目录帐户添加新订阅者。

1. 访问[批量许可服务中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx) (VLSC) 并登录。
2. 从 VLSC 管理页中，单击“订阅”  ，然后单击“Visual Studio 订阅”  。

    > [!div class="mx-imgBorder"]
    > ![“订阅”菜单](_img//vlsc/vlsc-subscriptions.png)

3. 单击与 Visual Studio 订阅相关联的“协议编号”  。

    > [!div class="mx-imgBorder"]
    > ![选择协议](_img/vlsc/vlsc-agreement.png)

4. 单击“分配订阅”  。
5. 选择所需的订阅级别  。
6. 验证你是否有可用于分配的订阅，然后单击“下一步”  。
7. 在“电子邮件地址”字段中，输入订阅者详细信息和目录地址，然后单击“下一步”  。
8. 验证订阅者信息，然后单击“完成”  。
9. 通知订阅者，订阅已通过使用下面的[模板](#notifying-your-subscribers-with-directory-addresses)进行预配。

### <a name="updating-an-existing-subscriber"></a>更新现有订阅者
请按照以下步骤更新现有订阅者的目录帐户。

1. 访问[批量许可服务中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx) (VLSC) 并登录。
2. 从 VLSC 管理页中，单击“订阅”  ，然后单击“Visual Studio 订阅”  。
3. 单击与 Visual Studio 订阅相关联的“协议编号”  。
4. 单击“搜索”栏上的向下箭头  。
5. 使用“电子邮件地址”字段搜索订阅者。
6. 从结果列表中，单击订阅者的“姓氏”  。
7. 单击“编辑”  。
8. 将“电子邮件地址”字段更改为所需的目录地址，然后单击“保存”  。
9. 通知订阅者，其订阅已通过使用下面的电子邮件模板进行预配。

### <a name="notifying-your-subscribers-with-directory-addresses"></a>通知订阅者目录地址
由于欢迎电子邮件无法成功发送给订阅者，请将以下邮件复制并粘贴到电子邮件中并发送给订阅者。 针对每个订阅者将 ％WORD％ 替换为适当的信息。

```
----------- Copy Below (Ctrl+C) -----------

Hello %SUBSCRIBER NAME%

You have been assigned a Visual Studio subscription. Please visit https://my.visualstudio.com, and log in with your %DIRECTORY ADDRESS% address to activate and access your subscription.

If you’re having trouble, please contact the support team (https://visualstudio.microsoft.com/subscriptions/support/).

At the bottom of the page, select the following:
   - Accounts, Subscriptions, and Billing Support
   - From Issue, choose Subscription sign in support
   - Choose the appropriate Country
   - Select the desired Assisted Support option

----------- End Copy -----------
```

## <a name="defining-a-work-or-school-account-as-a-personal-account"></a>将工作或学校帐户定义为个人帐户
请利用[将订阅者分配给目录帐户](#assigning-subscribers-to-a-directory-account)部分中所述的说明，在批量许可服务中心 (VLSC) 中添加新用户或更新用户的电子邮件地址。  在目录无法识别电子邮件地址的情况下，用户需要逐步完成此过程来创建一个新帐户，以将电子邮件地址定义为个人帐户。  就短期而言，Visual Studio 订阅团队已经获得了下面定义的标识策略的豁免，但是我们正在研发必要的功能来移除此策略。

> [!WARNING]
> Microsoft 不建议将“工作或学校”标识与“个人”标识并存。  这种操作会导致组织失去对账户的所有权和控制权，员工即使离开公司后也可以继续访问特定的产品或服务。  

### <a name="defining-an-email-address-as-a-personal-account"></a>将电子邮件地址定义为个人帐户
在向订阅者分配订阅后，他们将收到一封电子邮件，要求他们访问 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 以利用其订阅权益。  当尝试登录时，Visual Studio 订阅登录将失败，并显示一条错误，指出帐户无法识别。  在登录 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 之前，请要求订阅者遵循这些指示。  如有必要，可在分配订阅后使用此[模板](#notifying-your-subscribers-using-personal-accounts)来通知订阅者。

1. 导航到 https://my.visualstudio.com ，然后单击“创建新的 Microsoft 帐户”  。

2. 填写字段：
   - 在 Someone@example.com 框中输入接收欢迎电子邮件的电子邮件地址
   - 创建密码
   - 选择促销设置
   - 单击“下一步” 

3. 完成验证步骤，然后单击“下一步”  。

4. 新用户可能需要完成 Visual Studio 个人资料。

5. 现在应可以看到订阅和权益。

### <a name="notifying-your-subscribers-using-personal-accounts"></a>使用个人帐户通知订阅者
在上述情况中，订阅者将收到“欢迎电子邮件”，但由于存在别名，他们可能会发现自己无法登录。  你可以使用以下文本通知上述步骤中的订阅者，并根据需要推荐支持选项。  针对每个订阅者将 ％WORD％ 替换为适当的信息。

```
----------- Copy Below (Ctrl+C) -----------

Hello %SUBSCRIBER NAME%

You have been assigned a Visual Studio subscription, and may have been directed to log into https://my.visualstudio.com based on your Welcome email.  While this is the correct website for consuming benefits, our organization requires you to take a few extra steps before you can access the site.  Please follow the below instructions to help you create a “Microsoft Account” that is tied to our corporate email address.  Once these steps are completed, you will use your email address to access the Subscription benefits.
1. Visit https://my.visualstudio.com

2. Click Create new Microsoft Account on the right hand side

3. Complete the Form:
   - Use your corporate email address in the someone@example.com box
   - Enter a password
   - Select your promotional preference
   - Click Next

4. Complete the account validation steps

5. If necessary, complete the Visual Studio profile

6. You should now see your benefits

Note:  When visiting https://my.visualstudio.com in the future, you may be prompted to select which account you’d like to use (e.g. “Work or School Account” or “Personal Account”).  After following the steps above, you will need to leverage the “Personal Account” option.

If you’re having trouble, please contact the support team (https://visualstudio.microsoft.com/subscriptions/support/).

At the bottom of the page, select the following:
   - Accounts, Subscriptions, and Billing Support
   - From Issue, choose Subscription sign in support
   - Choose the appropriate Country
   - Select the desired Assisted Support option

----------- End Copy -----------
```
