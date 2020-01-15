---
title: 扩展试用版或更新许可证
description: 了解如何扩展免费试用版 Visual Studio，使用联机订阅或产品密钥解锁 Visual Studio，以及更新过时或过期的许可证。
ms.date: 12/18/2019
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: db0f75b3e4c2f066b7a9d79976a50efd3364d7bd
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591367"
---
# <a name="extend-a-trial-version-or-update-a-license"></a>扩展试用版或更新许可证

可以在 30 天内评估 [Visual Studio Professional 或 Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/compare/) 的免费试用版。 登录时，可以将试用期延长至 90 天。 （Visual Studio Community 是免费的，没有试用期。 但是，必须定期[登录](signing-in-to-visual-studio.md)，以使[许可证保持最新](#update-a-stale-license)。）

若要在试用期结束后继续使用 Visual Studio，请使用[在线订阅](#use-an-online-subscription)或[产品密钥](#enter-a-product-key)进行解锁。

## <a name="use-an-online-subscription"></a>使用在线订阅

1. 选择 IDE 右上角的“登录”  按钮（或转到“文件”   > “帐户设置”  ，打开“帐户设置”  对话框，然后选择“登录”  按钮）。

1. 对 Microsoft 帐户、工作或学校帐户输入凭据。 Visual Studio 将查找与帐户相关联的 Visual Studio 订阅或 Azure DevOps 组织。

> [!IMPORTANT]
> 当连接到“团队资源管理器”工具窗口的 Azure DevOps 组织时，Visual Studio 将自动查找相关联的在线订阅  。 当连接到 Azure DevOps 组织时，可以使用 Microsoft 帐户和工作或学校帐户登录。 如果该用户帐户有在线订阅，则 Visual Studio 将自动为你解锁 IDE。

有关 Visual Studio 订阅及其工作原理的详细信息，请参阅[订阅支持 FAQ](https://visualstudio.microsoft.com/subscriptions/support/) 页。

## <a name="enter-a-product-key"></a>输入产品密钥

1. 选择“文件”   > “帐户设置”  ，打开“帐户设置”  对话框，然后选择“使用产品密钥获得许可”  链接。

1. 在提供的空白处输入产品密钥。

> [!TIP]
> Visual Studio 的预发布版本没有产品密钥。 必须登录 IDE，才能使用预发布版本。

有关 Visual Studio 的 Visual Studio 产品密钥以及如何获取它们的详细信息，请参阅[使用 Visual Studio 订阅中的产品密钥 ](/visualstudio/subscriptions/product-keys)页。

## <a name="update-a-stale-license"></a>更新过时的许可证

你可能会在 Visual Studio 中看到一条消息，指示“许可证已过时，必须进行更新。”

![Visual Studio 过期许可证消息](../ide/media/vs2017_stale-license.png)

此消息表示你的订阅可能仍将有效，但 Visual Studio 用来保持订阅更新的许可证令牌尚未刷新。 Visual Studio 报告许可证过时是由于以下原因之一：

* 没有使用过 Visual Studio 或很长一段时间未连接到 Internet。
* 已注销 Visual Studio。

许可证令牌过期之前，Visual Studio 首先会显示警告消息，要求用户重新输入凭据。

如果不重新输入凭据，该令牌将开始过期倒计时，并且“帐户设置”  对话框会告知用户令牌在过期之前的剩余天数。 令牌过期后，必须重新输入帐户的凭据，然后才能继续使用 Visual Studio。

> [!Important]
> 如果在 Internet 访问有限或者没有 Internet 访问的环境中延长使用 Visual Studio，应使用产品密钥解锁 Visual Studio，以避免中断。

## <a name="update-an-expired-license"></a>更新已过期的许可证

订阅过期后，将不再具有 Visual Studio 的访问权限，必须续订或添加另一个具有订阅的帐户。 若要查看有关正在使用的许可证的详细信息，请转到“文件” > “帐户设置”，然后在该对话框的右侧查看许可证信息   。 如果用户拥有另一个与不同的帐户关联的订阅，请通过选择“添加帐户”链接，将该帐户添加到对话框左侧的“所有帐户”列表中   。

## <a name="get-support"></a>获取支持

有时会出现问题。 如果遇到问题，请参阅以下支持选项：

* 使用[报告问题](how-to-report-a-problem-with-visual-studio.md)工具报告产品问题。
* 在[订阅支持 FAQ](https://visualstudio.microsoft.com/subscriptions/support/) 中找到有关订阅、帐户和计费的问题解答。

## <a name="see-also"></a>请参阅

* [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)
* [比较 Visual Studio 版本](https://visualstudio.microsoft.com/vs/compare/)
* [了解有关 Visual Studio 订阅的详细信息](/visualstudio/subscriptions/)
