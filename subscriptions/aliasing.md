---
title: 使用别名登录 Visual Studio 订阅可能会失败 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 02/14/2020
ms.topic: conceptual
description: 如果别名或友好名称已被使用，登录可能会失败
ms.openlocfilehash: dff48852e566522ad01ee07bd46cda72b8e1e249
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77276619"
---
# <a name="signing-in-to-visual-studio-subscriptions-may-fail-when-using-aliases"></a>使用别名登录 Visual Studio 订阅可能会失败
根据用于登录的帐户类型，登录 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 时，可用订阅可能无法正确显示。 一个潜在的原因是使用了“别名”或“友好名称”来代替订阅所分配到的登录标识。 这就是所谓的“别名”。

## <a name="what-is-aliasing"></a>别名是什么？
“别名”一词是指具有不同身份的用户登录 Windows（或 Active Directory）并访问电子邮件。

当公司为其目录登录（例如“olivia@contoso.com”）提供 Microsoft Online Service 时，可能会遇到别名，但用户使用别名或友好名称（例如“OliviaG@contoso.com”）访问其电子邮件帐户。 请确保用户在 https://manage.visualstudio.com 使用 Visual Studio 订阅管理门户中列出的“登录电子邮件地址”登录以访问其订阅

## <a name="as-an-administrator-what-options-do-i-have"></a>作为管理员，有哪些选项可供我选择？

根据订阅者的帐户类型，在下面找到适用的解决方案：

### <a name="work-or-school-account-upn-mismatch-issue"></a>工作或学校帐户 UPN 不匹配问题

如果公司具有 Active Diretory 设置，而 UPN 与主 SMTP 地址不同，则可能会遇到用户主体名称 (UPN) 不匹配的问题。 

#### <a name="how-to-detect-if-a-users-sign-in-address-has-a-upn-mismatch"></a>如何检测用户的登录地址是否具有 UPN 不匹配的情况

让用户完成以下步骤：

1. 使用订阅分配电子邮件中提到的登录地址登录到 https://my.visualstudio.com 。  

    > [!NOTE]
    > 如果他们已找不到订阅分配电子邮件，你可以从管理门户中再次向其发送。  

2. 单击“订阅”选项卡  。
3. 验证显示在右上方的电子邮件地址（显示“您已登录为...”）与订阅分配电子邮件中的登录电子邮件地址是否相同。  如果不相同，他们将无法享受其订阅权益。 

   > [!div class="mx-imgBorder"]
   > ![“订阅”页](_img/aliasing/aliasing-subscriptions-page.png)

#### <a name="how-to-correct-the-upn-mismatch"></a>如何纠正 UPN 不匹配

1. 访问 Visual Studio 管理管理门户 https://manage.visualstudio.com 

2. 找到具有 UPN 不匹配问题的用户。  如果你有很多订阅，可通过[筛选](search-license.md)功能更轻松地找到用户。 

3. 将登录电子邮件地址更改为该用户的 UPN。

4. 保存更改 

5. 要求用户从订阅者门户注销并使用 UPN 再次登录。   

### <a name="personal-account-aliasing-issue"></a>个人帐户别名问题

别名问题也会影响个人帐户。 

#### <a name="how-to-detect-if-a-personal-account-has-an-aliasing-issue"></a>如何检测个人帐户是否有别名问题

1. 登录 https://my.visualstudio.com 。

2. 单击“订阅”选项卡，然后检查登录到的地址  。 

3. 如果登录电子邮件地址与用于访问网站的电子邮件地址不同，则帐户和别名之间存在冲突。 

#### <a name="how-to-fix-a-personal-account-aliasing-issue"></a>如何修复个人帐户别名问题

Visual Studio 订阅平台会排定主要别名的优先级，以显示订阅详细信息。  若要解决此问题，需要将其他电子邮件别名设为用于登录的主要别名。 

1. 转到[管理登录到 Microsoft 的方式](https://go.microsoft.com/fwlink/p/?linkid=842796)。
2. 如果系统提示，则登录到 Microsoft 帐户。 
3. 在“帐户别名”下，选择用于分配订阅的电子邮件旁的“设为主要”  。 
4. 在“帐户别名”下，选择用于分配订阅的电子邮件旁的“设为主要”。 
5. 从 Visual Studio 订阅者门户注销 (https://my.visualstudio.com) 
6. 使用新的主要别名再次访问门户。 

### <a name="ensure-a-successful-experience-for-your-users"></a>确保为用户提供登录成功的体验

作为管理员，可选择两种方式来确保你的订阅者在 https://my.visualstudio.com 上成功登录。 

- 第一个选项（推荐）是利用目录帐户作为 https://manage.visualstudio.com 的登录地址。
- 第二个选项（较不安全）允许订阅者使用目录电子邮件地址以外的电子邮件地址登录。

通过完成以下步骤在管理门户中配置这两个选项：

1. 登录到 https://manage.visualstudio.com 

2. 如果要更改单个用户，请在表中选中该用户，然后右键单击“编辑”。 这会打开一个面板，你可以在其中修改登录电子邮件地址。  

3. 在“登录电子邮件地址”字段中进行必要的更新。 

4. 单击“保存”，更改将生效。  
如果需要对大量用户进行这些更改，可以使用批量编辑功能。 有关此过程的详细信息，请参阅[编辑订阅](edit-license.md)文章的“使用批量编辑来编辑多个订阅”部分  。  

## <a name="next-steps"></a>后续步骤
了解有关管理 Visual Studio 订阅的详细信息。
- [分配单个订阅](assign-license.md)
- [分配多个订阅](assign-license-bulk.md)
- [编辑订阅](edit-license.md)
- [删除订阅](delete-license.md)
- [确定最大使用量](maximum-usage.md)

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)
