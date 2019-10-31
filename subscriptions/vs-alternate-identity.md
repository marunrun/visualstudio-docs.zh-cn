---
title: Visual Studio 订阅者标识
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/19/2019
ms.topic: conceptual
description: 如何为 Visual Studio 订阅添加用于登录 Azure DevOps 和 Azure 的备用标识
ms.openlocfilehash: e19774f2314280b2e5a995a7d83336f1403682a4
ms.sourcegitcommit: bcdab788085bd9931d73883fe70cd5831317dca2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72816554"
---
# <a name="identities-for-visual-studio-subscribers"></a>Visual Studio 订阅者标识
激活 Visual Studio 订阅时，我们会将用户激活期间使用的标识（或登录名）与 Visual Studio 订阅关联起来。 这样，我们便能在 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)、Azure DevOps 和 Azure 中识别你。

在 Azure DevOps 中，我们会在你每次登录时检查你的 Visual Studio 订阅状态，并在你所属的每个组织中自动授予相应功能。
由于这些功能是作为订阅者权益随附，因此可以在你使用与 Visual Studio 订阅关联的标识时，将你添加为任何 Azure DevOps 组织的成员。

在 Azure 中，用户激活其[每月 Azure 开发测试个人额度](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)（一项订阅者权益）时，我们会检查其 Visual Studio 订阅状态。

在 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)中，除激活过程中使用的标识外，还可添加“备用标识”  。 如果使用 Microsoft 帐户激活订阅，则可添加备用标识。 这样，你还能添加工作或学校帐户（登录 Visual Studio、Office 365 或公司/学校网络时使用的帐户），以使用个人帐户和工作或学校帐户访问 Azure DevOps。

## <a name="add-an-alternate-account-to-your-subscription"></a>向订阅添加备用帐户
在 Visual Studio 订阅中添加备用帐户后，可使用与订阅分配到的标识不同的标识享受订阅权益（如 Azure DevOps 和 Azure）。 在过去，仅当 Visual Studio (VS) 订阅已分配到 Microsoft 帐户 (MSA) 时此功能才可用。 我们已经将此功能扩展到 Azure Active Directory (Azure AD) 中的工作或学校帐户。

这不会向其他帐户提供订阅副本；它仅可使用备用帐户访问这两项权益。

对于所有订阅，都可添加“工作或学校帐户”，从而使用此帐户享受需要登录的权益（VS IDE、Azure DevOps 和 Azure）。

### <a name="add-the-alternate-account"></a>添加备用帐户
1. 使用 Microsoft 帐户 (https://my.visualstudio.com) 登录到 Visual Studio 订阅者门户。
2. 单击“订阅”选项卡  。
3. 选择“添加备用帐户”  。
4. 添加工作或学校帐户。
    > [!div class="mx-imgBorder"]
    > ![添加工作或学校帐户](_img/vs-alternate-identity/enter-alternate-account-my-visual-studio-com-portal.png)

5. 使用工作或学校帐户登录 Azure DevOps (https://{youraccount}.visualstudio.com)。
    > [!div class="mx-imgBorder"]
    > ![使用工作或学校帐户](_img/vs-alternate-identity/sign-in-with-alternate-account.png)

此时，备用帐户已添加到 Visual Studio 订阅中，可使用两个标识享受需要使用备用帐户登录的订阅权益（IDE、Azure DevOps 和 Azure）。

## <a name="faq"></a>FAQ

### <a name="q--why-doesnt-azure-devops-recognize-me-as-a-visual-studio-subscriber"></a>问：为什么 Azure DevOps 未将我识别为 Visual Studio 订阅者？

答：如果你使用主要标识或备用标识登录，Azure DevOps 应该会自动识别你的订阅。 如果没有，可尝试以下操作：

* 检查是否拥有包含 [Azure DevOps 权益](vs-azure-devops.md#eligibility)的有效 Visual Studio 订阅。

* 确认使用的登录名/标识是 Visual Studio 订阅的主要或备用标识。

* 登录 Azure DevOps 前，至少先访问一次 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)。

如果 Azure DevOps 仍无法识别你的订阅，请联系 [Azure DevOps 支持](https://azure.microsoft.com/support/devops/)。
