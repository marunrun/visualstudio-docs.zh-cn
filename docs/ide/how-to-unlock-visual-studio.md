---
title: 如何：解锁 Visual Studio
titleSuffix: ''
ms.date: 03/30/2019
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: fe0aa86be242e9a7e7ed8d877944c66247718167
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926293"
---
# <a name="how-to-unlock-visual-studio"></a>如何：解锁 Visual Studio

可以免费使用 Visual Studio 长达 30 天。 登录到 IDE 将试用期延长至 90 天。 若要继续使用 Visual Studio，请解锁 IDE，任选一种方法：

- 使用在线订阅

- 输入产品密钥

## <a name="to-unlock-visual-studio-using-an-online-subscription"></a>使用在线订阅解锁 Visual studio 的步骤

使用与 Microsoft 帐户或者工作或学校帐户相关联的 Visual Studio 订阅或 Azure DevOps 组织解锁 Visual Studio：

1. 选择 IDE 右上角的“登录”  按钮（或转到“文件”   > “帐户设置”  ，打开“帐户设置”  对话框，然后选择“登录”  按钮）。

1. 对 Microsoft 帐户、工作或学校帐户输入凭据。 Visual Studio 将查找与帐户相关联的 Visual Studio 订阅或 Azure DevOps 组织。

> [!IMPORTANT]
> 当连接到“团队资源管理器”工具窗口的 Azure DevOps 组织时，Visual Studio 将自动查找相关联的在线订阅  。 当连接到 Azure DevOps 组织时，可以使用 Microsoft 帐户和工作或学校帐户登录。 如果该用户帐户有在线订阅，则 Visual Studio 将自动为你解锁 IDE。

## <a name="to-unlock-visual-studio-with-a-product-key"></a>使用产品密钥解锁 Visual Studio

1. 选择“文件”   > “帐户设置”  ，打开“帐户设置”  对话框，然后选择“使用产品密钥获得许可”  链接。

1. 在提供的空白处输入产品密钥。

> [!TIP]
> Visual Studio 的预发布版本没有产品密钥。 必须登录 IDE，才能使用预发布版本。

## <a name="address-license-problem-states"></a>解决许可证的问题状态

### <a name="update-stale-licenses"></a>更新过时的许可证

你可能已见到过以下信息，指示许可证在 Visual Studio 中即将过时。 显示：“你的许可证已过期，必须进行更新。”

![Visual Studio 过期许可证消息](../ide/media/vs2017_stale-license.png)

此消息表示你的订阅可能仍将有效，但 Visual Studio 用来保持订阅更新的许可证令牌尚未刷新，且由于以下原因之一已过时：

- 没有使用 Visual Studio，或者没有用来延长时间的 Internet 连接。
- 已注销 Visual Studio。

许可证令牌过期之前，Visual Studio 首先会显示警告消息，要求用户重新输入凭据。

如果不重新输入凭据，该令牌将开始过期倒计时，并且“帐户设置”对话框会告知用户令牌在完全过期之前的剩余天数  。 令牌过期后，必须重新输入帐户的凭据，然后才能继续使用 Visual Studio。

> [!Important]
> 如果在 Internet 访问有限或者没有 Internet 访问的环境中延长使用 Visual Studio，应使用产品密钥解锁 Visual Studio，以避免中断。

### <a name="update-expired-licenses"></a>更新已过期的许可证

订阅完全过期后，将不再具有 Visual Studio 的访问权限，必须续订订阅或添加另一个具有订阅的帐户。 若要查看有关正在使用的许可证的详细信息，请转到“文件” > “帐户设置”，然后在该对话框的右侧查看许可证信息   。 如果用户拥有另一个与不同的帐户关联的订阅，请通过选择“添加帐户”链接，将该帐户添加到对话框左侧的“所有帐户”列表中   。

## <a name="see-also"></a>请参阅

* [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)
