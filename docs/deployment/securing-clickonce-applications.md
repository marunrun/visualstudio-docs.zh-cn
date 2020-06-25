---
title: 保护 ClickOnce 应用程序 | Microsoft Docs
ms.date: 02/17/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce security
- ClickOnce deployment, security
- deploying applications, ClickOnce security
ms.assetid: a05b5f2f-d1f2-471a-8096-8b11f7554265
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d99cbf4aaa30e1afb95a98743c223edee94d98fe
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286292"
---
# <a name="secure-clickonce-applications"></a>保护 ClickOnce 应用程序
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序受 .NET Framework 中代码访问安全性约束的限制，以帮助限制代码访问受保护的资源和操作的权限。 因此，了解代码访问安全性的含义以相应地编写 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是十分重要的。 您的应用程序可以使用完全信任或使用部分区域（如 Internet 区域和 Intranet 区域）来限制访问权限。

 此外，ClickOnce 使用证书验证应用程序发行者的真实性，并使用证书为应用程序和部署清单签名，以证明文件未被篡改。 签名是一个可选的步骤，它会使在生成清单以后更改应用程序文件更容易。 然而，在没有签名清单的情况下，很难确保应用程序安装程序在受到中间人安全攻击时不被篡改。 出于这个原因，我们建议您对应用程序清单和部署清单进行签名，以帮助保护您的应用程序。

## <a name="zones"></a>区域
 使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 技术部署的应用程序被限定为由安全区域定义的一组权限和操作。 安全区域在 Internet Explorer 中定义，并基于应用程序的位置。 下表列出基于部署位置的默认权限：

|部署位置|安全区域|
|-------------------------|-------------------|
|从 Web 运行|Internet 区域|
|从 Web 安装|Internet 区域|
|从网络文件共享安装|本地 Intranet 区域|
|从 CD-ROM 安装|完全信任|

 默认权限取决于部署初始应用程序版本的位置；应用程序的更新将继承这些权限。 如果将应用程序配置为从 Web 或网络位置检查是否有更新且存在较新的版本，则初始安装可以获得 Internet 或 Intranet 区域的权限，而不是完全信任权限。 如果不想让系统提示用户，系统管理员可以指定一个 ClickOnce 部署策略，将某个特定的应用程序发行者定义为受信任的来源。 对于部署此策略的计算机，系统会自动授予权限而不会提示用户授予权限。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。 若要配置受信任的应用程序部署，可以将证书安装到计算机或企业级别。 有关详细信息，请参阅 [How to: Add a Trusted Publisher to a Client Computer for ClickOnce Applications](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)。

## <a name="code-access-security-policies"></a>代码访问安全性策略
 应用程序的权限取决于应用程序清单的[ \<trustInfo> 元素](../deployment/trustinfo-element-clickonce-application.md)元素中的设置。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会根据项目的 **“安全性”** 属性页上的设置自动生成此信息。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序仅被授予它所请求的特定权限。 例如，文件访问需要完全信任权限时，如果应用程序请求文件访问权限，则它仅被授予文件访问权限，而不会被授予完全信任权限。 在开发 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，你应确保仅请求应用程序需要的特定权限。 在大多数情况下，你可以使用 Internet 区域和本地 Intranet 区域来将你的应用程序限制为部分信任。 有关更多信息，请参阅[如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)。 如果应用程序需要自定义权限，则您可以创建一个自定义区域。 有关详细信息，请参阅[如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)。

 如果包括应用程序部署区域的默认权限集以外的权限，则会导致在安装或更新时提示最终用户授予权限。 如果不想让系统提示用户，系统管理员可以指定一个 ClickOnce 部署策略，将某个特定的应用程序发行者定义为受信任的来源。 在部署此策略的计算机上，系统会自动授予权限而不会提示用户授予权限。

 作为开发人员，您有责任确保您的应用程序将以适当的权限运行。 如果应用程序在运行时请求区域之外的权限，则可能会出现安全性异常。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]使你能够在目标安全区域中调试应用程序，并提供有关开发安全应用程序的帮助。 有关详细信息，请参阅[调试使用 system.web 的 ClickOnce 应用程序](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)。

 有关代码访问安全性和 ClickOnce 的详细信息，请参阅[ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)。

## <a name="code-signing-certificates"></a>代码签名证书
 若要使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署发布应用程序，可以用公钥/私钥对为应用程序的应用程序和部署清单签名。 **“项目设计器”** 的 **“签名”** 页上提供了用于为清单签名的工具。 有关更多信息，请参见 [Signing Page, Project Designer](../ide/reference/signing-page-project-designer.md)。

 为清单签名之后，安装期间，权限对话框将向用户显示基于 Authenticode 签名的发行者信息，以向用户表明该应用程序来自受信任的来源。

 有关 ClickOnce 和证书的更多信息，请参见 [ClickOnce and Authenticode](../deployment/clickonce-and-authenticode.md)。

## <a name="aspnet-form-based-authentication"></a>ASP.NET 基于窗体的身份验证
 如果要控制每个用户能访问哪些部署，则不应允许对 Web 服务器上部署的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序进行匿名访问。 而应根据用户的身份使用 Windows 身份验证允许用户访问已安装的部署。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用持久性 Cookie，所以它不支持基于 ASP.NET 窗体的身份验证；这些 Cookie 会带来安全风险，因为它们驻留在 Internet Explorer 缓存中，可能受到攻击。 因此，如果部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，将不支持除 Windows 身份验证以外的任何身份验证方案。

## <a name="pass-arguments"></a>传递参数
 如果必须将参数传递到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序中，则将出现一项额外的安全性注意事项。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使开发人员可以向部署在 Web 上的应用程序提供查询字符串。 该查询字符串采用了在用于启动应用程序的 URL 末尾跟随一系列名称/值对的形式：

 `http://servername.adatum.com/WindowsApp1.application?username=joeuser`

 默认情况下，查询字符串参数处于禁用状态。 若要启用查询字符串，则必须在应用程序部署清单中设置特性 `trustUrlParameters` 。 此值可通过 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 和 MageUI.exe 来设置。 有关如何启用传递查询字符串的详细步骤，请参阅[如何在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。

 在未检查参数以确保参数安全的情况下，决不要将通过查询字符串检索的参数传递给数据库或命令行。 不安全参数是包含数据库或命令行转义符的参数，这些转义符可以让恶意用户操纵应用程序执行任意命令。

> [!NOTE]
> 查询字符串参数是在启动时向 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序传递参数的唯一途径。 不能从命令行向 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序传递参数。

## <a name="deploying-obfuscated-assemblies"></a>部署经过模糊处理的程序集
 Visual Studio 包括免费的 [PreEmptive Protection - Dotfuscator Community](../ide/dotfuscator/index.md)，使用它，可以通过代码混淆和主动保护措施来保护 ClickOnce 应用程序。  有关详细信息，请参阅 [Dotfuscator Community 用户指南的 ClickOnce 部分](https://www.preemptive.com/dotfuscator/ce/docs/help/5.27/advanced_clickonce.html)。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
