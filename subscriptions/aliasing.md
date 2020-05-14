---
title: 使用别名登录 Visual Studio 订阅可能会失败 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 97bf7474-c6c2-49b3-b2c9-f1b2808eed1a
ms.date: 03/02/2020
ms.topic: conceptual
description: 如果别名或友好名称已被使用，登录可能会失败
ms.openlocfilehash: 0f5ed4fe67dbd863a7ba4c22f10946cbeb1c36b0
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "79509052"
---
# <a name="signing-into-visual-studio-subscriptions-may-fail-when-using-aliases"></a>使用别名登录 Visual Studio 订阅可能会失败
根据用于登录的帐户类型，登录 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 时，可用订阅可能无法正确显示。 一个潜在的原因是使用了“别名”或“友好名称”来代替订阅所分配到的登录标识。 这就是所谓的“别名”。

## <a name="what-is-aliasing"></a>别名是什么？
“别名”一词是指具有不同身份的用户登录 Windows（或 Active Directory）并访问电子邮件。

当公司为其目录登录（例如“JohnD@contoso.com”）提供 Microsoft Online Service 时，可能会遇到别名，但用户使用别名或友好名称（例如“John.Doe@contoso.com”）访问其电子邮件帐户。 请确保用户使用管理门户中列出的”登录电子邮件地址”(https://manage.visualstudio.com) 访问其订阅。 

## <a name="what-are-the-potential-issues"></a>潜在问题是什么？

根据订阅者的帐户类型，他们可能会遇到以下两个问题之一。 

### <a name="work-or-school-account-upn-mismatch-issue"></a>工作或学校帐户 UPN 不匹配问题 
如果公司具有 Active Diretory 设置，而 UserPrincipalName (UPN) 与主 SMTP 地址不同，则可能会遇到 UPN 不匹配的问题。 

#### <a name="how-to-detect-if-your-sign-in-address-is-impacted-by-a-upn-mismatch"></a>如何检测登录地址是否受 UPN 不匹配问题的影响 

1. 使用订阅分配电子邮件中提到的登录地址登录到 https://my.visualstudio.com/subscriptions。

2. 验证页面右上角列出的登录电子邮件地址是否与你用于登录的地址匹配。  如果不匹配，则你的 UPN 不匹配，你将无法查看订阅。 

> [!div class="mx-imgBorder"]
> ![登录电子邮件地址](_img//aliasing/sign-in-email.png)

#### <a name="how-to-fix-a-upn-mismatch"></a>如何修复 UPN 不匹配的问题

1. 访问 Visual Studio 管理门户 [https://manage.visualstudio.com](https://manage.visualstudio.com) 

2. 找到具有 UPN 不匹配问题的订阅者。 （使用[筛选器](search-license.md)功能可以轻松地查找订阅者。）

3. 将登录电子邮件地址更改为订阅者的 UPN 

0. 保存更改 

0. 通知订阅者从订阅者门户注销，然后使用 UPN 再次访问 

### <a name="personal-account-aliasing-issue"></a>个人帐户别名问题

如果用于登录 Visual Studio 订阅门户的电子邮件地址与订阅关联的电子邮件地址不匹配，那么个人订阅帐户也会遇到问题。 

#### <a name="how-to-detect-if-your-personal-subscription-account-is-impacted-by-an-aliasing-issue"></a>如何检测个人订阅帐户是否受别名问题影响

1. 登录到 [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions)

0. 验证页面右上角列出的登录电子邮件地址是否与你用于登录的地址匹配。  如果登录电子邮件地址与用于访问网站的电子邮件地址不同，则帐户和别名之间存在冲突。

#### <a name="how-to-fix-an-alias-issue"></a>如何修复别名问题

Visual Studio 平台会排定主要别名的优先级，以显示订阅详细信息。 

1. 转到**管理登录到 Microsoft 的方式**。 如果系统提示，则登录到 Microsoft 帐户。 

2. 在“帐户别名”下，选择用于分配订阅的电子邮件旁的“设为主要”。 

> [!div class="mx-imgBorder"]
> ![设置主电子邮件地址](_img//aliasing/account-aliases.png)

3. 从 Visual Studio 订阅门户 (https://my.visualstudio.com)) 注销 

4. 使用用于分配订阅的帐户重新登录，该帐户现在应配置为主要别名。 

## <a name="preventing-aliasing-issues"></a>防止出现别名问题

作为管理员，有两种选择可确保你的订阅者在 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 上成功登录。
- 第一种选择（推荐）是将目录帐户用作 Visual Studio 订阅门户 (https://my.visualstudio.com) 的登录名。  
- 第二种选择（较不安全）是允许订阅者使用目录电子邮件地址以外的电子邮件地址登录。

通过完成以下步骤，可以在管理门户中配置这两个选项：  
1. 登录 [https://manage.visualstudio.com](https://manage.visualstudio.com) 

0. 如果要更改单个用户，请在表中选中该用户，然后右键单击“编辑”。 这会打开一个面板，你可以在其中修改登录电子邮件地址。 在“登录电子邮件地址”字段中进行必要的更新。 单击“保存”，更改将生效。  

0. 如果需要对大量用户进行这些更改，可以使用批量编辑功能。 有关详细信息，请阅读[使用批量编辑功能编辑多个订阅者](https://docs.microsoft.com/visualstudio/subscriptions/edit-license#edit-multiple-subscribers-using-bulk-edit)一文。

> [!NOTE]
> 不管是使用单独更改还是批量更改，订阅者都会收到一封电子邮件，其中说明已更改其登录电子邮件地址，并提示他们需要使用更新后的电子邮件地址登录。 另请注意，如果订阅者以前通过其他登录地址激活了权益，则需要继续使用该登录地址来访问权益。  

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


