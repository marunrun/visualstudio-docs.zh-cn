---
title: 登录 Visual Studio 订阅时遇到的问题 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 176c7f11-b19d-49e9-a6dd-b2e5da5e8480
ms.date: 03/11/2020
ms.topic: conceptual
description: 了解登录 Visual Studio 订阅时可能出现的问题
ms.openlocfilehash: de27f64f1d5c83ed01a1e561f4921dbed53c479c
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233246"
---
# <a name="issues-signing-in-to-visual-studio-subscriptions"></a>登录 Visual Studio 订阅时遇到的问题
若要使用 Visual Studio 订阅，必须先登录。  根据订阅，你可能已使用 Microsoft 帐户 (MSA) 或 Azure Active Directory (AAD) 标识进行设置。  本文讨论了在登录订阅时可能遇到的一些问题。

## <a name="microsoft-accounts-msa-cannot-be-created-using-workschool-email-addresses"></a>无法使用工作/学校电子邮件地址创建 Microsoft 帐户 (MSA)
在 Azure AD 中配置电子邮件域时，不再允许使用工作/学校电子邮件地址创建新的个人 Microsoft 帐户 (MSA)。 这是什么意思呢？ 如果你的组织在使用 Microsoft 365 的 Office 365 或其他业务服务时依赖于 Azure AD，且你已向 Azure AD 租户添加了域名，则用户将无法再使用你域中的电子邮件地址创建新的个人 Microsoft 帐户。

### <a name="why-was-this-change-made"></a>为什么要进行此更改？
将工作地址作为用户名的个人 Microsoft 帐户会出现许多最终用户和 IT 部门的问题。 例如：
- 用户可能会认为他们的个人 Microsoft 帐户符合业务要求，并且当他们将业务文档保存到 OneDrive 中时，也是满足符合性的
- 离开组织的用户通常会失去对其工作电子邮件地址的访问权限。 当他们这样做时，如果忘记密码，则可能无法找回他们的个人 Microsoft 帐户。 另一方面，IT 部门可以重置密码并进入前雇员的个人帐户。
- IT 部门对帐户所有权和安全性有一种错觉。 但用户只需将代码往返到工作电子邮件地址一次，则可以在将来随时重命名其帐户。

对于拥有两个具有相同电子邮件地址的帐户（一个 Azure AD 和一个 Microsoft 帐户），情况尤其令人困惑。

### <a name="what-does-this-experience-look-like"></a>这是种什么体验？
如果你尝试使用工作或学校电子邮件地址注册 Microsoft 使用者应用，将看到以下消息。

   > [!div class="mx-imgBorder"]
   > ![无法使用工作电子邮件创建帐户](_img/sign-in-issues/cannot-use-work-email.png)

但是，如果你尝试注册支持个人和工作/学校帐户的 Microsoft 应用，应看到以下消息：

   > [!div class="mx-imgBorder"]
   > ![支持工作或学校帐户](_img/sign-in-issues/existing-account.png)

### <a name="are-existing-accounts-affected"></a>现有帐户是否受影响？
此处描述的注册块仅阻止创建新帐户。 它对已拥有工作/学校电子邮件地址的 Microsoft 帐户的用户没有影响。 如果你已处于这种情况，我们已改进，你可以更轻松地重命名个人 Microsoft 帐户。 这篇[支持文章](https://windows.microsoft.com/en-US/Windows/rename-personal-microsoft-account)提供了简单的逐步指导。 重命名个人 Microsoft 帐户意味着更改用户名，不会影响工作电子邮件或登录到业务服务（如 Office 365）的方式。 它也不会影响个人资料 - 只是改变了登录方式。 你可以使用其他（个人）电子邮件地址，从 Microsoft 获取新的 @outlook.com 电子邮件地址，或将电话号码用作新用户名。

> [!NOTE]
> 如果 IT 部门要求使用工作/学校电子邮件创建个人 Microsoft 帐户，例如访问 Microsoft 业务服务（如顶级支持），请在重命名帐户之前与管理团队联系。

## <a name="deleting-a-sign-in-address-may-prevent-access-to-a-subscription"></a>删除登录地址可能会阻止访问订阅
如果删除与订阅关联的一个或多个标识（MSA 或 AAD），则你的订阅者信息（包括用户名和登录 ID）可能会呈现匿名，从而导致无法访问订阅。

为避免对订阅访问权限产生影响，请使用以下方法之一。
- 部署单一标识管理系统（MSA 或AAD），但不能同时部署这两者。
- 通过租户关联 AAD 和 MSA 标识。

## <a name="signing-in-may-fail-when-using-aliases"></a>使用别名时，登录可能会失败
根据用于登录的帐户类型，登录 [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) 时，可用订阅可能无法正确显示。 一个潜在的原因是使用了“别名”或“友好名称”来代替订阅所分配到的登录标识。 这就是所谓的“别名”。

### <a name="what-is-aliasing"></a>别名是什么？
“别名”一词是指具有不同身份的用户登录 Windows（或 Active Directory）并访问电子邮件。

当公司为其目录登录（例如 JohnD@contoso.com）提供 Microsoft Online Service 时，可能会遇到别名，但用户使用别名或友好名称（例如 John.Doe@contoso.com）访问其电子邮件帐户。 对于通过批量许可服务中心 (VLSC) 管理其订阅的许多客户来说，由于提供的电子邮件地址 (John.Doe@contoso.com) 与通过“工作或学校帐户”选项成功进行身份认证所需的目录地址 (JohnD@contoso.com) 不匹配，这种做法可能会导致登录失败。

### <a name="what-options-do-i-have"></a>我有哪些选择？
从订阅者的角度来看，首先与管理员配合来了解贵公司的标识配置非常重要。 如有必要，管理员必须从其管理门户更新你的帐户设置，或者你需要使用公司电子邮件地址创建 Microsoft 帐户 (MSA)。 在采取措施创建 MSA 之前，请先与你的管理员讨论采取此操作的任何策略或问题。 

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 了解如何在 AAD 中[关联 MSA 和 AAD 帐户](/azure/active-directory/b2b/add-users-administrator)。
- 详细了解[授权](anonymization.md)。
