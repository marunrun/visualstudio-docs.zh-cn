---
title: 使用多个用户帐户
ms.date: 07/23/2019
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 872089158b6e4dc0b55c26ad187e3b68d0501f26
ms.sourcegitcommit: b2fc9ac7d73c847508f6ed082bed026476bb3955
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2020
ms.locfileid: "77027596"
---
# <a name="work-with-multiple-user-accounts"></a>使用多个用户帐户

如果有多个 Microsoft 帐户和/或单位或学校帐户，可将它们全部添加到 Visual Studio，以便可从任何帐户访问资源，而无需单独登录到这些帐户。 Azure、Application Insights、Azure DevOps 和 Office 365 服务都支持简化的登录体验。

将多个帐户添加到一台计算机上之后，如果你在另一台计算机上登录到 Visual Studio，则该组帐户会随你一起漫游。

> [!NOTE]
> 尽管帐户名可漫游，但凭据却不能。 第一次尝试在新的计算机上使用其资源时，将提示你输入这些其他帐户的凭据。

本文介绍如何将多个帐户添加到 Visual Studio。 还显示如何查看可从“添加连接的服务”对话框、“服务器资源管理器”和“团队资源管理器”等位置的帐户访问的资源    。

## <a name="sign-in-to-visual-studio"></a>登录 Visual Studio

使用 Microsoft 帐户或组织帐户登录到 Visual Studio。 窗口上方会显示你的用户名，类似于：

![当前登录的用户](../ide/media/vs2015_username.png)

### <a name="access-your-azure-account-in-server-explorer"></a>在服务器资源管理器中访问你的 Azure 帐户

若要打开服务器资源管理器，请选择“查看” > “服务器资源管理器”   （或者，如果使用的是“常规”[环境设置](../ide/environment-settings.md)  ，请按 Ctrl+Alt+S）   。 展开“Azure”节点，注意它包含 Azure 帐户中可用的资源，该资源与用于登录 Visual Studio 的帐户相关联  。 它看上去类似于下图：

![展开了 Azure 节点的服务器资源管理器](../ide/media/work-with-multiple-user-accounts/server-explorer.png)

在任何特定设备上首次使用 Visual Studio 时，对话框都将只显示在登录的账户下注册的订阅。 通过右键单击“Azure”节点、选择“管理和筛选订阅”并从帐户选取器控件添加帐户，可以直接从“服务器资源管理器”访问任何其他帐户的资源    。 如果需要，可以通过单击向下箭头，从帐户列表中选择另一个帐户。 选择帐户之后，可以自定义帐户下的哪些订阅在“服务器资源管理器”中显示  。

![“管理 Azure 订阅”对话框](../ide/media/vs2015_manage_subs.png)

下次打开“服务器资源管理器”时，将显示所选订阅的资源  。

### <a name="access-your-azure-account-via-add-connected-service-dialog"></a>通过“添加连接的服务”对话框，访问你的 Azure 帐户

1. 打开一个现有项目，或创建一个新项目。

1. 选择“解决方案资源管理器”中的项目节点，然后右键单击并选择“添加” > “连接的服务”    。

   随即出现“添加连接的服务”向导，其中显示与 Visual Studio 个性化账户相关联的 Azure 帐户中的服务列表  。 无需单独登录 Azure。 但是，第一次尝试从另一计算机访问其资源时，你需要登录到其他帐户。

### <a name="access-azure-active-directory-in-a-web-project"></a>在 Web 项目中访问 Azure Active Directory

Azure Active Directory (AAD) 支持 ASP.NET MVC web 应用中的最终用户单一登录或 Web API 服务中的 AD 身份验证。 域身份验证与单个用户帐户身份验证不同。 有权访问 Active Directory 域的用户可以使用其现有的 AAD 帐户连接到 web 应用程序。 Office 365 应用还可以使用域身份验证。

::: moniker range="vs-2017"

要了解此操作，请创建一个新的“ASP.NET Core Web 应用程序”项目  。 在“新建 ASP.NET Core Web 应用程序”对话框中，选择“Web 应用程序”模板，然后选择“更改身份验证”    。

::: moniker-end

::: moniker range=">=vs-2019"

要了解此操作，请创建一个新的“ASP.NET Core Web 应用程序”项目  。 在“创建新 ASP.NET Core Web 应用程序”页中，选择“Web 应用程序”模板，然后在“身份验证”下选择“更改”     。

::: moniker-end

随即显示“更改身份验证”对话框，你可以在该对话框中选择要在应用程序中使用的身份验证类型  。

![适用于 ASP.NET 的更改身份验证对话框](../ide/media/vs2015_change_authentication.png)

有关 ASP.NET 中不同类型的身份验证的详细信息，请参阅[在 Visual Studio 中创建 ASP.NET web 项目](/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#authentication-methods)。

### <a name="access-your-azure-devops-organization"></a>访问 Azure DevOps 组织

在主菜单中，选择“团队” > “管理连接”以打开“团队资源管理器 - 连接”窗口    。 选择“管理连接” > “连接到项目”   。 在“连接到项目”对话框中，从列表中选择一个项目（或选择“添加 TFS 服务器”并输入服务器的 URL）   。 选择 URL 后，无需重新输入凭据即可登录。

有关详细信息，请参阅[连接到团队资源管理器中的项目](connect-team-project.md)。

## <a name="add-an-additional-account-to-visual-studio"></a>向 Visual Studio 添加另一个帐户

若要将其他帐户添加到 Visual Studio：

1. 选择“文件” > “帐户设置”   。

1. 在“所有帐户”下，选择“添加帐户”   。

1. 在“登录到你的帐户”页面上，选择该帐户或选择“使用另一个帐户”   。 按照提示输入新的帐户凭据。

（可选）现在可以转到“服务器资源管理器”，并查看与刚添加的帐户相关联的 Azure 服务  。 在“服务器资源管理器”中，右键单击“Azure”节点并选择“管理和筛选订阅”    。 通过单击当前帐户旁的下拉箭头选择新的帐户，然后选择想要在“服务器资源管理器”中显示的订阅  。 应可以看到与指定订阅关联的所有服务。 即使当前未使用第二个帐户登录到 Visual Studio，也可登录到该帐户的服务和资源。 “项目”   > “添加连接的服务”  和“团队”   > “连接到 Team Foundation Server”  也是如此。

### <a name="add-an-account-using-device-code-flow"></a>使用设备代码流添加帐户

在某些情况下，无法以常规方式登录或添加帐户。 如果 Internet Explorer 因某种原因被阻止，或网络设置了防火墙，则可能发生这种情况。 要解决此问题，可以启用“设备代码流”来添加帐户或重新验证帐户  。 借助设备代码流，可使用另一种浏览器或在另一个物理或虚拟 (VM) 机&mdash;上登录。

使用设备代码流登录：

1. 打开“工具” > “选项” > “环境”下的 [“帐户”](reference/accounts-environment-options-dialog-box.md)页面，然后选择“在添加或重新验证帐户时启用设备代码流”      。 选择“确定”关闭选项页  。

1. 选择“文件” > “帐户设置”以打开帐户管理页面   。

1. 在“所有帐户”下，选择“添加帐户”   。

   会出现一个对话框，其中显示了要粘贴到 web 浏览器中的 URL 和代码。

   ![设备代码流 URL 和代码](media/work-with-multiple-user-accounts/device-login-code.png)

1. 按“Ctrl+C”复制对话框文本，然后选择“确定”关闭对话框    。 将复制的文本粘贴到文本编辑器（如记事本）中。 这使得在下一步中复制代码更加容易。

1. 导航到机器或 web 浏览器上用于登录到 Visual Studio 的设备登录 URL，然后将复制的代码粘贴或输入到“代码”框中  。

   “Visual Studio”应用名称应会显示在页面的更下方  。

1. 在“Visual Studio”下，选择“继续”   。

   ![device-login-page.png](media/work-with-multiple-user-accounts/device-login-page.png)

1. 按照提示输入帐户凭据。

   随即出现一个页面，提示已在设备上登录 Visual Studio，可以关闭浏览器窗口。

   ![通过浏览器登录 visual Studio 这一操作已完成](media/work-with-multiple-user-accounts/sign-in-browser-complete.png)

1. 返回 Visual Studio 中的帐户管理页面，其中的“所有帐户”下列出了新添加的帐户  。 选择“关闭”  。

## <a name="see-also"></a>请参阅

- [登录 Visual Studio](signing-in-to-visual-studio.md)
- [登录 Visual Studio for Mac](/visualstudio/mac/signing-in)
