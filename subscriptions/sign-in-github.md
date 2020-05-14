---
title: 使用 GitHub 帐户登录到 Visual Studio 订阅 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 1bdcb3c9-bba1-4e25-a609-9d7e539d78e0
ms.date: 03/09/2020
ms.topic: conceptual
description: 了解如何使用 GitHub 帐户登录到 Visual Studio 订阅。
ms.openlocfilehash: 722eeae315a8b4a6bd93fb1048846b147b294afa
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233228"
---
# <a name="signing-in-to-visual-studio-subscriptions-with-your-github-account"></a>使用 GitHub 帐户登录到 Visual Studio 订阅 

登录到 Visual Studio 订阅的步骤取决于你所使用的帐户类型。 例如，你可能正在使用由你的公司或学校提供的 Microsoft 帐户 (MSA) 或电子邮件地址。 自 2019 年 1 月起，现还可使用 GitHub 帐户登录某些订阅。 

本文将提供使用 GitHub 帐户登录的步骤。

## <a name="signing-in-with-your-github-account"></a>使用 GitHub 帐户登录

借助 GitHub 标识支持，可使用现有的 GitHub 帐户作为新的或现有的 Microsoft 帐户的凭据，将 GitHub 帐户与 Microsoft 帐户链接。 

使用 GitHub 登录时，Microsoft 会检查与 GitHub 帐户关联的任何电子邮件地址是否与现有的个人或企业 Microsoft 帐户相匹配。 如果地址与企业帐户匹配，系统会提示你改为登录该帐户。 如果地址与个人帐户匹配，我们会将你的 GitHub 帐户添加为该个人帐户的登录方法。

在 GitHub 与 Microsoft 帐户凭据链接后，可在任何可使用个人 Microsoft 帐户的地方使用该单一登录，例如 Azure 站点、Office 应用和 Xbox。 假设电子邮件地址与邀请的电子邮件地址匹配，这些帐户还可以作为 Microsoft 帐户用于 Azure Active Directory 来宾登录。

> [!NOTE]
> 将 GitHub 标识链接到 Microsoft 帐户不会授予 Microsoft 任何代码访问权限。 当 Azure DevOps 和 Visual Studio 等应用需要访问代码存储库时，系统会提示你授予对此次访问的特定许可。 

### <a name="frequently-asked-questions"></a>常见问题
以下常见问题解答可解决你在使用 GitHub 帐户凭据登录 Visual Studio 订阅时可能遇到的问题。

#### <a name="q-i-forgot-my-github-password--how-can-i-access-my-account-now"></a>问：我忘记了 GitHub 密码。  现如何访问我的帐户？
答：可转到 [Reset your password](https://github.com/password_reset)（重置密码），恢复 GitHub 帐户。 或者可以通过在[恢复你的帐户](https://account.live.com/password/reset)输入 GitHub 帐户的电子邮件地址，恢复与 GitHub 链接的 Microsoft 帐户。

#### <a name="q-i-deleted-my-github-account--how-can-i-access-my-microsoft-account-msa-now"></a>问：我已删除我的 GitHub 帐户。  现如何访问我的 Microsoft 帐户 (MSA)？
答：如果没有 MSA 的任何其他凭据（如密码、Authenticator 应用或安全密钥），则可以使用附加到 Microsoft 帐户上的电子邮件地址来恢复该帐户。 要开始使用，请转到[恢复你的帐户](https://account.live.com/password/reset)。 必须为帐户添加密码，这样我们就能知道以后如何让你登录。 

#### <a name="q-theres-no-sign-in-with-github-option-on-the-sign-in-page--how-can-i-use-my-github-credentials-to-sign-in"></a>问：登录页面上没有“使用 GitHub 登录”选项。  如何使用我的 GitHub 凭据进行登录？
答：键入在创建 GitHub 链接的 Microsoft 帐户时选择的 GitHub 帐户电子邮件地址。 我们将向你发送信息，让你前往 GitHub 进行登录。 或者，如果登录页面上有登录选项链接，请使用单击该链接后显示的“使用 GitHub 登录”按钮  。 

#### <a name="q-i-cant-sign-in-to-some-of-my-apps-and-products-with-github--why"></a>问：我无法使用 GitHub 登录我的某些应用和产品。  为什么？
答：并非所有 Microsoft 产品都可以通过其登录页面访问 GitHub.com，例如 Xbox 控制台。 相反，在从链接的 GitHub 帐户键入电子邮件地址时，我们会向该地址发送代码，以便确认是否是你本人。 你只需使用其他登录方法登录同一帐户。 

#### <a name="q--ive-added-a-password-to-the-microsoft-account-i-have-linked-to-my-github-account--will-that-cause-a-problem"></a>问：我已将密码添加到已链接到我的 GitHub 帐户的 Microsoft 帐户。  这是否会出现问题？
答：完全不需要。 这不会更改你的 GitHub 密码；你只是具有另一种方式登录 Microsoft 帐户。 每当你使用电子邮件地址登录时，我们都会为你提供使用 Microsoft 帐户密码登录或前往 GitHub 登录的选项。 我们强烈建议，如果需要添加密码，请确保该密码与 GitHub 帐户的密码不同。

#### <a name="q-i-want-to-add-the-authenticator-app-to-the-account-i-created-using-github--can-i-do-that"></a>问：我想将 Authenticator 应用添加到我使用 GitHub 创建的帐户。  我是否可以执行此操作？
答：没问题，只需下载应用并使用你的电子邮件地址登录即可。 使用电子邮件地址登录时，系统会提示你选择 [Authenticator 应用](https://www.microsoft.com/p/microsoft-authenticator/9nblgggzmcj6)或 GitHub 作为你的凭据。

#### <a name="q-ive-enabled-two-factor-authentication-on-both-my-github-and-microsoft-accounts-msa-but-when-i-sign-in-to-my-msa-im-still-asked-to-authenticate-twice--why"></a>问：我对我的 GitHub 和 Microsoft 帐户 (MSA) 都启用了双因素身份验证，但是当我登录 MSA 时，我仍需要进行两次身份验证。  为什么？
答：由于安全限制，即使对帐户启用了双重验证，Microsoft 也会将使用 GitHub 登录视为单因素验证。 因此，必须再次对 Microsoft 帐户进行身份验证。 

#### <a name="q--how-can-i-tell-if-my-microsoft-account-and-github-accounts-are-linked"></a>问：如何判断我的 Microsoft 帐户是否已与 GitHub 帐户链接？
答：每当你使用帐户别名（电子邮件地址、电话号码、Skype 名称）进行签名时，我们都会向你显示帐户的所有登录方法。 如果未在此看到 GitHub，那么你还未进行设置。

#### <a name="q--how-can-i-unlink-my-microsoft-and-github-accounts"></a>问：如何取消 Microsoft 和 GitHub 帐户的链接？ 
答：转到 account.microsoft.com 的[“安全”选项卡](https://account.microsoft.com/security)，然后单击“更多安全选项”，以取消链接 GitHub 帐户  。 取消链接 GitHub 帐户会将其从登录方法中删除，并且会删除对 Visual Studio 中任何 GitHub 存储库的访问权限。 其他 Microsoft 产品可能已请求单独访问你的 GitHub 帐户，因此删除此处的访问权限不会删除在所有产品中的访问权限。 转到 GitHub 配置文件的[应用程序权限](https://github.com/settings/applications)页，从其中所列的应用中撤销许可。

#### <a name="q--i-try-to-use-my-github-account-to-sign-in-but-im-prompted-that-i-already-have-a-microsoft-identity-that-i-should-use-instead--whats-happening"></a>问：我尝试使用我的 GitHub 帐户登录，但系统提示我已经拥有一个 Microsoft 标识，我应该改用该标识。  发生了什么情况？
答：如果你的 GitHub 帐户具有 Azure Active Directory 电子邮件地址，则表示你已拥有可以使用 GitHub 代码访问 Azure 并运行 CI 管道的 Microsoft 标识。 使用该帐户可确保你的 Azure 资源和生成管道保留在组织边界内。 但如果你正在从事个人工作，我们建议在 GitHub 帐户中添加个人电子邮件地址，这样你始终可以访问该帐户。 执行此操作后，请尝试再次登录，并在系统提示你登录工作或学校帐户时选择“使用其他电子邮件地址”  。 这将让你使用该个人电子邮件地址创建新的 Microsoft 帐户。

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
成功登录到订阅门户后，建议访问 https://my.visualstudio.com/benefits 上的“权益”页，并浏览适合你的强大工具、服务和产品。  
