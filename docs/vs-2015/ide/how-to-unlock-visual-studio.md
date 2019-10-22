---
title: 解锁 Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a71a045661c48fd36733ecd8d2266470667a5c35
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670598"
---
# <a name="how-to-unlock-visual-studio"></a>如何解锁 Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以免费使用 Visual Studio 长达 30 天。 登录 IDE 时，可以将试用期延长 90 天。 若要继续使用 Visual Studio，可以解锁 IDE，方法是

1. 使用在线订阅。

2. 输入产品密钥。

## <a name="to-unlock-visual-studio-using-an-online-subscription"></a>使用在线订阅解锁 Visual studio 的步骤
 使用 MSDN 或者与 Microsoft 帐户、工作或学校帐户相关联的 Visual Studio 在线订阅解锁 Visual Studio：

1. 单击 IDE 右上角的“登录”按钮（或转到“文件”>“帐户设置”，以打开“帐户设置”对话框，然后单击"登录"按钮。）

2. 对 Microsoft 帐户、工作或学校帐户输入凭据。 Visual Studio 将查找 MSDN 订阅或与你的帐户相关联的 Visual Studio Team Services 订阅。

> [!IMPORTANT]
> 当连接到“团队资源管理器”工具窗口的 Visual Studio Team Services 帐户时，Visual Studio 将自动查找相关联的在线订阅。 当连接到 Visual Studio Team Services 帐户时，可以使用 Microsoft 和工作或学校帐户登录。 如果该用户帐户有在线订阅，则 Visual Studio 将自动为你解锁 IDE。

## <a name="to-unlock-visual-studio-with-a-product-key"></a>使用产品密钥解锁 Visual Studio

1. 选择“文件”>“帐户设置”  ，打开“帐户设置”对话框并单击“使用产品密钥获得许可”  链接。

2. 在提供的空白处输入产品密钥。

> [!TIP]
> Visual Studio 的预发布版本没有产品密钥。 必须登录 IDE，才能使用预发布版本。

## <a name="addressing-license-problem-states"></a>解决许可证问题状态

### <a name="updating-stale-licenses"></a>更新过期的许可证
 你可能已见到过以下信息 - 许可证在 Visual Studio 中即将过时。

 ![Visual Studio“用户信息”对话框](../ide/media/vs2013-userinfo.png "|::ref1::|")

 此消息表示你的订阅可能仍将有效，但 Visual Studio 用来保持订阅更新的许可证令牌尚未刷新，且由于以下原因之一已过时：

1. 没有使用 Visual Studio，或者没有用来延长时间的 Internet 连接。

2. 已注销 Visual Studio。

   许可证令牌过期之前，Visual Studio 将首先显示警告消息，要求你重新输入凭据。

   如果不重新输入凭据，则令牌将过期。 发生这种情况时，“帐户设置”对话框将显示距令牌完全过期还有多少天。 令牌过期后，需要使用以上另一种方法重新对此帐户或许可证输入凭据，然后才能继续使用 Visual Studio。

> [!IMPORTANT]
> 如果在有限或者没有 Internet 访问的环境中延长使用 Visual Studio，应该使用产品密钥解锁 Visual Studio，以避免中断。

### <a name="updating-expired-licenses"></a>更新已过期的许可证
 如果你的订阅已完全过期，你不再具有 Visual Studio 的访问权限，必须：

1. 续订你的订阅 若要查看有关正在使用的许可证的详细信息，请转到“文件”>“帐户设置”对话框，然后在该对话框的右侧查看许可证信息。

2. 如果拥有另一个与不同的帐户相关联的订阅，请通过单击“添加帐户...”链接，将该帐户添加到“文件”>“帐户设置”对话框左侧的“所有帐户” 列表中。

## <a name="see-also"></a>另请参阅
 [登录 Visual Studio](../ide/signing-in-to-visual-studio.md)
