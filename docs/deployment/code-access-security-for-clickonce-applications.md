---
title: 点击次数应用程序的代码访问安全性 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vb.XBAPProjectPropertiesSecurity.HowTo
- vb.XBAProjectPropertiesSecurity.HowTo
- vb.ProjectPropertiesSecurity.HowTo
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], security
- ClickOnce applications, caspol
- security [ClickOnce], WPF browser-hosted applications
- security [ClickOnce], ClickOnce applications
- ClickOnce applications, code access security policies
- security, ClickOnce
ms.assetid: 04b104d0-0bd3-4ccb-b164-1de92d234487
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9fd2d9b6792cae002967c9000474a825bd3a0651
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649281"
---
# <a name="code-access-security-for-clickonce-applications"></a>ClickOnce 应用程序的代码访问安全性
ClickOnce 应用程序基于 .NET Framework，需遵从代码访问安全性约束。 因此，了解代码访问安全性的含义并且相应地编写 ClickOnce 应用程序是十分重要的。

 代码访问安全性是 .NET Framework 中的一种机制，它帮助限制代码对受保护的资源和操作的访问权限。 你应该为 ClickOnce 应用程序配置代码访问安全性权限，以使用适合应用程序安装程序位置的区域。 在大多数情况下，你可以选择 **“Internet”** 区域获得有限的权限集，或者选择 **“本地 Intranet”** 区域获得更大的权限集。

## <a name="default-clickonce-code-access-security"></a>默认的 ClickOnce 代码访问安全性
 默认情况下，在客户端计算机上安装或运行 ClickOnce 应用程序时，它会获得完全信任权限。

- 具有完全信任权限的应用程序可以不受限制地访问文件系统和注册表等资源。 这可能会导致你的应用程序（和最终用户的系统）被恶意代码利用。

- 当应用程序需要完全信任权限时，可能会提示最终用户向其授予对该应用程序的权限。 这意味着应用程序不会真正提供 ClickOnce 体验，并且该提示可能会给经验较少的用户造成混淆。

  > [!NOTE]
  > 当从可移动媒体（如 CD-ROM）安装应用程序时，将不会提示用户。 此外，网络管理员可以配置网络策略，以便在从受信任的源安装应用程序时不会提示用户。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

  若要限制 ClickOnce 应用程序的权限，可以修改应用程序的代码访问安全性权限，以请求最适合你的应用程序所需权限的区域。 在大多数情况下，你可以选择从中部署该应用程序的区域。 例如，如果你的应用程序是企业应用程序，则可以使用 **“本地 Intranet”** 区域。 如果你的应用程序是 Internet 应用程序，则可以使用 **“Internet”** 区域。

## <a name="configure-security-permissions"></a>配置安全权限
 你始终应该配置 ClickOnce 应用程序，以请求适当的区域来限制代码访问安全性权限。 可以在 **“项目设计器”** 的 **“安全”** 页上配置安全性权限。

 **“项目设计器”** 中的 **“安全”** 页包含 **“启用 ClickOnce 安全设置”** 复选框。 选中此复选框后，安全权限请求会添加到应用程序的部署清单。 安装时，如果请求的权限超出从中部署该应用程序的区域的默认权限，则会提示用户授予权限。 有关详细信息，请参阅[如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)。

 从不同位置部署的应用程序不经提示就会授予不同级别的权限。 例如，从 Internet 部署应用程序时，它会获得高度受限的权限集。 从本地 Intranet 安装时，它会获得更多权限，从 CD-ROM 安装时，它会获得完全信任权限。

 作为配置权限的起始点，你可以从 **“安全”** 页上的 **“区域”** 列表选择一个安全区域。 如果可能将从多个区域部署你的应用程序，请选择具有最少权限的区域。 有关更多信息，请参阅[如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)。

 可以设置的属性随着权限集变化；并非所有权限集都具有可配置属性。 有关你应用程序可以请求的权限的完整列表的详细信息，请参阅 <xref:System.Security.Permissions>。 有关如何为自定义区域设置权限的详细信息，请参阅[如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)。

## <a name="debug-an-application-that-has-restricted-permissions"></a>调试具有受限权限的应用程序
 作为开发人员，很可能以完全信任权限运行你的开发计算机。 因此，调试应用程序时你不会看到与用户在使用受限权限运行应用程序时可能看到的安全性异常相同的安全性异常。

 为了捕获这些异常，你必须使用与最终用户相同的权限来调试应用程序。 可以在 **“项目设计器”** 的 **“安全”** 页上启用使用受限权限进行调试。

 当你使用受限权限调试应用程序时，尚未在 **“安全”** 页上启用的任意代码安全性需求都会引发异常。 将出现一个异常帮助程序，提供有关如何修改你的代码以避免此异常的建议。

 此外，在编写代码时，代码编辑器中的 IntelliSense 功能将禁用未包含在已配置安全权限中的任意成员。

 有关更多信息，请参见 [如何：使用受限权限对 ClickOnce 应用程序进行调试](securing-clickonce-applications.md)。

## <a name="security-permissions-for-browser-hosted-applications"></a>浏览器托管的应用程序的安全权限
 Visual Studio 为 Windows Presentation Foundation (WPF) 应用程序提供了以下项目类型：

- WPF Windows 应用程序

- WPF Web 浏览器应用程序

- WPF 自定义控件库

- WCF 服务库

  在这些项目类型中，只有 WPF Web 浏览器应用程序托管在 Web 浏览器中，因此需要特殊的部署和安全设置。 这些应用程序的默认安全设置如下：

- **启用"单击一次安全设置"**

- **这是部分信任应用程序**

- **“Internet 区域”** （具有选定的 WPF Web 浏览器应用程序的默认权限集）

  在 **“高级安全设置”** 对话框中， **“使用所选的权限集调试此应用程序”** 复选框被选中然后禁用。 这是因为不能关闭浏览器托管的应用程序的“在区域中调试”。

## <a name="see-also"></a>另请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：为 ClickOnce 应用程序设置自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限对 ClickOnce 应用程序进行调试](securing-clickonce-applications.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [”项目设计器“ -&gt;“安全”页](../ide/reference/security-page-project-designer.md)