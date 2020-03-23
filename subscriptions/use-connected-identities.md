---
title: 如何使用连接的 Microsoft 帐户和 Azure Active Directory 标识 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/11/2020
ms.topic: conceptual
robots: noindex, nofollow
description: 了解如何使用已连接的 Microsoft 帐户和 Azure Active Directory 标识
ms.openlocfilehash: 3dcb41a26f27e5135962edf7ff933de40ccefe5e
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "79508974"
---
# <a name="how-to-use-connected-identities-in-visual-studio-subscriptions"></a>如何在 Visual Studio 订阅中使用连接的标识
如果你通过工作或学校收到 Visual Studio 订阅，并使用你的 Microsoft 帐户 (MSA) 登录，则你的订阅管理员可能会将你的 MSA 连接到组织的 Azure Active Directory (Azure AD) 中的标识。  这会改变你访问订阅中包含的一些权益的方式。 

## <a name="overview-of-connected-ids"></a>连接的 ID 概述
组织越来越多地转向基于 Azure AD 的标识，从而为自动管理订阅提供改进的安全性和支持。  如果你的订阅使用 MSA（如 @outlook.com 或其他个人电子邮件地址），则管理员可能会将登录电子邮件更改为你的 Azure AD 标识。  这会改变如何登录到订阅者门户 https://my.visualstudio.com ，但可能不会更改你访问所有权益的方式。  

如果管理员连接你的 MSA 和 Azure AD 标识，你将收到一封电子邮件，告知你使用 Azure AD 标识（而不是 MSA）开始访问 Visual Studio 订阅。 

## <a name="how-to-access-benefits-using-azure-ad-identities"></a>如何使用 Azure AD 标识访问权益
管理员将你的 MSA 连接到 Azure AD 标识后，你需要使用 Azure AD 标识登录到订阅者门户 https://my.visualstudio.com ，以访问基于 Azure AD 的权益。  这些方法包括：
- Visual Studio IDE
- Azure DevOps
- Azure 开发测试个人额度

## <a name="how-to-access-benefits-using-your-msa"></a>如何使用 MSA 访问权益
若要获取 Visual Studio 订阅中提供的许多权益（如 Pluralsight、LinkedIn 和 CloudPilot 等），你实际上会在合作伙伴的网站上创建用户帐户。  对于这些帐户，你应继续使用创建帐户时所用的标识。  例如，如果使用 MSA 激活了 Pluralsight 权益，无论用于登录到订阅者门户的标识如何，都应在进行 Pluralsight 培训时继续使用 MSA。  

## <a name="use-an-alternate-identity-to-access-your-subscription"></a>使用备用标识访问订阅
在 Visual Studio 订阅中添加备用帐户后，可使用与订阅分配到的标识不同的标识享受订阅权益（如 Azure DevOps 和 Azure）。 在过去，仅当 Visual Studio (VS) 订阅已分配到 Microsoft 帐户 (MSA) 时此功能才可用。 我们已经将此功能扩展到 Azure Active Directory (Azure AD) 中的工作或学校帐户。  有关使用备用帐户的详细信息，请查看我们的[备用标识](vs-alternate-identity.md)文章。 

## <a name="frequently-asked-questions"></a>常见问题
### <a name="q-how-can-i-contact-my-admin-about-this"></a>问：如何联系管理员以了解这一点？
答：有关联系管理员的信息，请参阅[联系订阅管理员](contact-my-admin.md)文章。  

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
管理员连接 Azure AD 和 MSA 帐户后，我们建议验证你是否可以登录到[订阅门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)并访问 Azure DevOps、Visual Studio 和 Azure 开发测试个人额度等权益。 