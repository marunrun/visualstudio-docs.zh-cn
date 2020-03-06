---
title: 登录 Visual Studio
titleSuffix: ''
ms.custom: seodec18
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 48c3ad98043947d9153c1fb9c406a60e5ae8839a
ms.sourcegitcommit: b016ea260856264eee730ee8cbcab198314a7ece
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "77904100"
---
# <a name="sign-in-to-visual-studio"></a>登录 Visual Studio

通过登录到个性化帐户，可以个性化和优化 Visual Studio 中的开发体验。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[登录到 Visual Studio for Mac](/visualstudio/mac/signing-in)。

## <a name="why-should-i-sign-in-to-visual-studio"></a>我为什么应该登录到 Visual Studio？

登录后，可获得丰富的 Visual Studio 体验。 例如，登录后，可以跨设备[同步设置](synchronized-settings-in-visual-studio.md)、延长试用期，以及自动连接到 Azure 服务等。

以下是登录后可体验的内容及可执行的操作的完整列表：
- **延长 Visual Studio 试用期** - 可将 Visual Studio Professional 或 Visual Studio Enterprise 的使用延长 90 天，而不会限定为 30 天试用期。 有关详细信息，请参阅[延长试用版期限或更新许可证](../ide/how-to-unlock-visual-studio.md)。

- **解锁 Visual Studio Community Edition** - 如果 Community Edition 安装提示需要许可证，请登录 IDE 自行解锁。

- 如果使用与 Microsoft Visual Studio 订阅或 Azure DevOps 组织相关联的帐户，解锁 Visual Studio  。 有关详细说明，请参阅[延长试用版期限或更新许可证](../ide/how-to-unlock-visual-studio.md)。

- **访问 Visual Studio Dev Essentials 程序的权限** - 此程序包括免费软件产品/服务、培训、支持等。 请参阅 [Visual Studio Dev Essential](https://visualstudio.microsoft.com/dev-essentials/) 了解详细信息。

- **同步 Visual Studio 设置** - 登录到任何设备上的 Visual Studio 时，将立即应用自定义设置（例如，键绑定、窗口布局和颜色主题）。 请参阅 [Visual Studio 中的同步设置](../ide/synchronized-settings-in-visual-studio.md)。

- 在 IDE 中自动连接到服务（如 Azure 和 Azure DevOps Services），而不会再次提示对同一帐户输入凭据。 

## <a name="how-to-sign-in-to-visual-studio"></a>如何登录到 Visual Studio

首次打开 Visual Studio 时，系统将要求登录并提供一些基本注册信息。 

![登录提示](../ide/media/vs2019_signinpopup.png)

应选择最符合需求的 Microsoft 帐户或工作（学校）帐户。 如果你没有此类帐户，可以单击“登录”按钮下的链接，免费创建一个 Microsoft 帐户。 如果遇到问题，请参阅[如何注册 Microsoft 帐户？](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)

然后，选择要在 Visual Studio 中使用的 UI 设置和颜色主题。 Visual Studio 会记住这些设置并将其同步到登录到的所有 Visual Studio 环境。 有关已同步的设置列表，请参阅[已同步的设置](../ide/synchronized-settings-in-visual-studio.md)。 以后可以打开 Visual Studio 中的“工具” > “选项”菜单来更改设置   。

提供设置后，Visual Studio 将启动，然后你就会进行登录并准备好开始操作。 若要验证你是否已登录，请在 Visual Studio 环境的右上角查找名称。

![VS2019 中当前已登录的用户](../ide/media/vs2019_username.png)

如果你选择在首次打开 Visual Studio 时不登录，可以在以后轻松登录。 查找 Visual Studio 环境的右上角中的“登录”  链接。 

![不是已登录用户](../ide/media/vs2019_usernotsignedin.png)

除非注销，否则在启动 Visual Studio 时会自动登录，并自动应用于对同步设置所做的所有更改。 若要注销，请单击 Visual Studio 环境右上角显示个人资料名称的图标，然后依次选择“帐户设置”命令和“注销”链接   。 若要再次登录，请选择 Visual Studio 环境的右上角中的 **“登录”** 命令。

## <a name="to-change-your-profile-information"></a>更改你的配置文件信息

1. 转到“文件” > “帐户设置”，然后选择“管理 Visual Studio 配置文件”链接    。

1. 在浏览器窗口，选择“编辑配置文件”并更改所需的设置  。

1. 完成后，选择“保存更改”  。

## <a name="troubleshooting"></a>疑难解答

如果在登录时遇到任何问题，请参阅[订阅支持](https://visualstudio.microsoft.com/subscriptions/support/)页获取帮助。

## <a name="see-also"></a>请参阅

* /[扩展试用版或更新许可证](../ide/how-to-unlock-visual-studio.md)
* [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)
* [登录 (Visual Studio for Mac)](/visualstudio/mac/signing-in)
* [激活 (Visual Studio for Mac)](/visualstudio/mac/activation)
