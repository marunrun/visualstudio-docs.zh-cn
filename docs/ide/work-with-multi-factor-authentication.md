---
title: 适用于需要多重身份验证的帐户
ms.date: 05/27/2020
ms.topic: conceptual
description: 了解如何将 Visual Studio 与需要多重身份验证的帐户一起使用。
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 699580689bcf00d00d2a6e07f814be4d1265bb1d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283541"
---
# <a name="how-to-use-visual-studio-with-accounts-that-require-multi-factor-authentication"></a>如何将 Visual Studio 与需要多重身份验证的帐户一起使用

在与外部来宾用户协作时，最好使用条件访问 (CA) 策略（例如多重身份验证 (MFA)）来保护你的应用和数据 。  

启用后，来宾用户不仅需要用户名和密码来访问你的资源，而且还必须满足其他安全要求。 可在租户、应用或个人来宾用户级别上强制实施 MFA 策略，操作方式与为你自己的组织成员启用这些策略的方式相同。 

## <a name="how-is-the-visual-studio-experience-affected-by-mfa-policies"></a>MFA 策略会对 Visual Studio 体验带来什么影响？
与启用了 CA 策略（例如 MFA）并与两个或多个租户相关联的帐户一起使用时，Visual Studio 16.6 之前的版本可能会降低身份验证体验。

这些问题可能会导致你的 Visual Studio 实例每天多次提示重新验证。 你可能必须重新输入之前已经过身份验证的租户的凭据，即使在同一个 Visual Studio 会话过程中也是如此。

## <a name="using-visual-studio-with-mfa-policies"></a>搭配使用 Visual Studio 与 MFA 策略
在 Visual Studio 2019 16.6 版本中，我们添加了新的功能，该功能简化了用户对受 CA 策略（如 MFA）保护资源的访问方式。 要使用此增强工作流，需要选择使用系统的默认 Web 浏览器作为添加并重新验证 Visual Studio 帐户的机制。  

> [!WARNING]
> 如果未使用此工作流，则在添加或重新验证 Visual Studio 帐户时，可能会触发降级的体验，导致多次额外的身份验证提示。 

### <a name="enabling-system-web-browser"></a>启用系统 Web 浏览器

> [!NOTE] 
> 为了获得最佳体验，建议在继续此工作流之前清除系统的默认 Web 浏览器数据。 此外，如果 Windows 10 设置中的“访问工作或学校”下有工作或学校帐户，请验证它们是否已正确通过身份验证。

要启用此工作流，请转到 Visual Studio 的“选项”对话框（“工具”>“选项…”），选择“帐户”选项卡，然后在“使用以下方式添加并重新验证帐户:”下拉列表中选取“系统 Web 浏览器”   。 

:::image type="content" source="media/select-system-web-browser.png" alt-text="从菜单中选择系统 Web 浏览器。":::

### <a name="sign-into-additional-accounts-with-mfapolicies"></a>使用 MFA 策略登录其他帐户 
启用系统 Web 浏览器工作流后，可以通过“帐户设置”对话框（“文件”>“帐户设置…”）按常规方式登录或向 Visual Studio 添加帐户。   
</br>
:::image type="content" source="media/add-personalization-account.png" alt-text="向 Visual Studio 添加新的个性化帐户。" border="false":::

此操作将打开系统的默认 Web 浏览器，要求你登录帐户，并验证任何所需的 MFA 策略。

根据你的开发活动和资源配置，系统可能会提示你在会话期间重新输入凭据。 当你添加新资源或尝试访问资源时，如果之前未满足其 CA/MFA 授权要求，可能会发生这种情况。

> [!NOTE] 
> 为了获得最佳体验，请保持浏览器打开，直到为资源验证了所有 CA/MFA 策略。 关闭浏览器可能会导致以前生成的 MFA 状态丢失，并且可能会提示其他授权提示。

## <a name="reauthenticating-an-account"></a>重新验证帐户  
如果你的帐户有问题，Visual Studio 可能会要求你重新输入帐户凭据。  

:::image type="content" source="media/reauthenticate-account.png" alt-text="重新验证 Visual Studio 帐户。":::

单击“重新输入凭据”会打开系统的默认 Web 浏览器，并尝试自动刷新你的凭据。 如果失败，系统将要求登录你的帐户并验证任何所需的 CA/MFA 策略。

> [!NOTE] 
> 为了获得最佳体验，请保持浏览器打开，直到为资源验证了所有 CA/MFA 策略。 关闭浏览器可能会导致以前生成的 MFA 状态丢失，并且可能会提示其他授权提示。

## <a name="how-to-opt-out-of-using-a-specific-azure-active-directory-tenant-in-visual-studio"></a>如何在 Visual Studio 中选择退出使用特定的 Azure Active Directory 租户

Visual Studio 2019 16.6 版能够更灵活地筛选特定租户，从而将其隐藏在 Visual Studio 中。 筛选出特定租户后，无需再向该租户进行身份验证，但这也意味着你将无法访问任何关联资源。 

当你有多个租户并且想要通过面向特定的子集来优化开发环境时，此功能很有用。 在无法验证特定 CA/MFA 策略的情况下，此功能也很有用，因为你可以筛选出违规的租户。 

### <a name="how-to-filter-out-a-tenant"></a>如何筛选出租户
要筛选与你的 Visual Studio 帐户关联的租户，请打开“帐户设置”对话框（“文件”>“帐户设置…”）并单击“应用筛选器” 。 
</br>
</br>

:::image type="content" source="media/apply-filter.png" alt-text="应用筛选器。" border="false":::

此时将显示“筛选帐户”对话框，让你选择要与帐户一起使用的租户。 

:::image type="content" source="media/select-filter-account.png" alt-text="选择要筛选的帐户。":::

## <a name="see-also"></a>请参阅

- [登录 Visual Studio](signing-in-to-visual-studio.md)
- [登录 Visual Studio for Mac](/visualstudio/mac/signing-in)
- [使用多个用户帐户](work-with-multiple-user-accounts.md)
