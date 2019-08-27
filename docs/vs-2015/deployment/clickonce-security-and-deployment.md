---
title: ClickOnce 安全和部署 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployment
- deploying applications [ClickOnce]
- ClickOnce deployment
- publishing, ClickOnce
ms.assetid: abab6d34-c3c2-45c1-a8b6-43c7d3131e7a
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 592bf358c24bee146290e8b3a00e28a0870f452d
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263804"
---
# <a name="clickonce-security-and-deployment"></a>ClickOnce 安全和部署
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 是一种部署技术，可用于创建自我更新的基于 Windows 的应用程序可以安装和运行时最少的用户交互。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用于发布和更新部署使用 ClickOnce 技术，如果您已开发您的项目与 Visual Basic 和 Visual C# 应用程序提供全面支持。 有关部署 Visual 信息C++应用程序，请参阅[视觉对象的 ClickOnce 部署C++应用程序](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署克服了部署中的三个主要问题：  
  
- **更新应用程序的困难。** 使用 Microsoft Windows Installer 部署，每当更新应用程序时，用户可以安装更新，一个 msp 文件，并将其应用于已安装的产品;使用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署，你可以提供自动更新。 下载仅这些应用程序的已更改部分，并从新的并行文件夹然后重新安装完整的更新应用程序。  
  
- **对用户的计算机的影响。** 使用 Windows 安装程序部署时，应用程序通常依赖于共享组件，可能会版本控制冲突;使用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署中，每个应用程序是自包含且不能干扰其他应用程序。  
  
- **安全权限。** Windows Installer 部署要求管理权限，并允许只有受限的用户安装;[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署可以让非管理用户安装并仅授予这些代码访问安全性权限，应用程序。  
  
  在过去，这些问题有时会导致开发人员可以决定创建 Web 应用程序而不是基于 Windows 的应用程序，会牺牲的安装便利的丰富用户界面。 通过使用应用程序使用部署[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]，您可以充分利用这两种技术。  
  
## <a name="what-is-a-clickonce-application"></a>什么是 ClickOnce 应用程序？  
 一个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序是任何 Windows Presentation Foundation (.xbap)、 Windows 窗体 (.exe)、 控制台应用程序 (.exe) 或使用发布 Office 解决方案 (.dll)[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]技术。 您可以将发布[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]三种不同方式应用程序： 在网页上，从网络文件共享，或从 cd-rom 介质。 一个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序可以安装在最终用户的计算机上和本地运行，即使计算机处于脱机状态，或者它可以在仅限联机使用的模式下运行，而无需最终用户计算机上永久安装任何内容。 有关详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 可以自更新应用程序;它们可以检查较新版本可用，并且自动替换所有更新的文件。 开发人员可以指定更新行为；网络管理员也可以控制更新策略，如将更新标记为强制性更新。 更新可以也将回滚到较早版本的最终用户或管理员。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。  
  
 因为[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序是独立安装或运行[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序不能破坏现有应用程序。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序是独立;每个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]安装到和从安全每个用户，每个应用程序缓存中运行应用程序。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 在 Internet 或 Intranet 安全区域中运行应用程序。 必要时，应用程序可以请求提升的安全权限。 有关详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。  
  
## <a name="how-clickonce-security-works"></a>ClickOnce 安全的工作原理  
 核心[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]基于安全证书、 代码访问安全策略和 ClickOnce 信任提示。  
  
### <a name="certificates"></a>证书  
 验证码证书用于验证应用程序的发行者的真实性。 通过对应用程序部署使用验证码，ClickOnce 可帮助阻止有害程序饰演本身为来自可信任的源的合法程序。 （可选） 还可以使用证书为应用程序签名和部署清单，以证明文件未被篡改。 有关详细信息，请参阅[ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)。 证书还用于配置客户端计算机具有受信任的发布服务器的列表。 如果应用程序来自受信任的发行者，则它可以安装无需任何用户交互。 有关详细信息，请参阅 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。  
  
### <a name="code-access-security"></a>代码访问安全性  
 代码访问安全性帮助限制代码对受保护资源的访问权限。 在大多数情况下，可以选择 Internet 或本地 Intranet 区域来限制权限。 使用**安全**页面**ProjectDesigner**请求适合于应用程序的区域。 此外可以调试具有受限的权限来模拟最终用户体验的应用程序。 有关详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)。  
  
### <a name="clickonce-trust-prompt"></a>ClickOnce 信任提示  
 如果应用程序请求更多的权限超出允许的区域，可以提示最终用户做出信任决策。 最终用户可以决定是否信任，可以运行 ClickOnce 应用程序，如 Windows 窗体应用程序、 Windows Presentation Foundation 应用程序、 控制台应用程序、 XAML 浏览器应用程序，和 Office 解决方案。 有关详细信息，请参阅[如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。  
  
## <a name="how-clickonce-deployment-works"></a>ClickOnce 部署的工作原理  
 核心[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署体系结构基于两个 XML 清单文件： 应用程序清单和部署清单。 这些文件用于描述从何处安装 ClickOnce 应用程序、 更新的方式和更新时。  
  
### <a name="publishing-clickonce-applications"></a>发布 ClickOnce 应用程序  
 应用程序清单描述应用程序本身。 这包括程序集、 依赖项和文件组成应用程序、 所需的权限，以及更新将在其中可用的位置。 应用程序开发人员编写应用程序清单中使用 Visual Studio 或清单生成和编辑工具 (Mage.exe) 中的发布向导[!INCLUDE[winsdklong](../includes/winsdklong-md.md)]。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。  
  
 部署清单描述应用程序的部署方式。 这包括应用程序清单的位置和客户端应运行的应用程序的版本。  
  
### <a name="deploying-clickonce-applications"></a>部署 ClickOnce 应用程序  
 创建后，部署清单复制到部署位置。 该位置可以是 Web 服务器、网络文件共享或媒体（如 CD）。 应用程序清单和应用程序的所有文件也会复制到部署清单中指定的部署位置。 该位置可以与部署清单的部署位置相同，也可以不同。 使用时**发布向导**在 Visual Studio 中，复制操作，将自动执行。  
  
### <a name="installing-clickonce-applications"></a>安装 ClickOnce 应用程序  
 部署到部署位置后，最终用户可以下载并安装应用程序，通过单击表示部署清单文件，在网页上或文件夹中的图标。 在大多数情况下，最终用户提供一个简单的对话框，要求用户确认安装，此后的安装过程继续进行，并且该应用程序已启动而无需额外的干预。 在其中应用程序需要提升的权限，或如果应用程序不由受信任的证书签名的情况下，对话框中还会要求用户授予权限，然后才能继续安装。 尽管 ClickOnce 安装是每个用户，如果有需要管理员权限的先决条件可能所需权限提升。 有关提升权限的详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。  
  
 证书可以是受信任在计算机或企业级别，以便使用受信任的证书签名的 ClickOnce 应用程序可以以无提示方式安装。 有关受信任的证书的详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。  
  
 可以将应用程序添加到用户的**启动**菜单并对其**添加或删除程序**组中**控制面板**。 与其他部署技术，执行任何操作添加到**Program Files**文件夹或注册表中，并且没有管理权限所需的安装  
  
> [!NOTE]
> 还有可能阻止应用程序添加到**启动**菜单并**添加或删除程序**组中，有效并且它类似于 Web 应用程序。 有关详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。  
  
### <a name="updating-clickonce-applications"></a>更新 ClickOnce 应用程序  
 当应用程序开发人员创建应用程序的更新的版本时，它们生成一个新的应用程序清单，并将文件复制到部署位置-通常是原始应用程序部署文件夹的同级文件夹。 管理员将更新部署清单，以指向新版本的应用程序的位置。  
  
> [!NOTE]
> **发布向导**在 Visual Studio 中可用于执行这些步骤。  
  
 除了部署位置，部署清单还包含应用程序在其中检查更新版本的更新位置 （网页或网络文件共享）。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] **发布**属性用于指定应用程序时间和频率应检查更新。 可以在部署清单中，指定更新行为或其形式可以是通过应用程序的用户界面中的用户选择[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]Api。 此外，Publish 属性还可用于将更新设置为强制执行，或用于将应用程序回滚到较早版本  。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。  
  
### <a name="third-party-installers"></a>第三方安装程序  
 您可以自定义 ClickOnce 安装程序，以安装第三方组件以及您的应用程序。 必须具有可再发行组件包 （.exe 或.msi 文件），并描述具有一个非特定于语言的产品清单和特定于语言的包清单包。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。  
  
## <a name="clickonce-tools"></a>ClickOnce 工具  
 下表显示的工具可用于生成、 编辑、 登录，并对应用程序和部署清单重新签名。  
  
|Tool|描述|  
|----------|-----------------|  
|[“项目设计器”->“安全”页](../ide/reference/security-page-project-designer.md)|登录应用程序和部署清单。|  
|[“项目设计器”->“发布”页](../ide/reference/publish-page-project-designer.md)|生成和编辑 Visual Basic 和 Visual C# 应用程序的应用程序和部署清单。|  
|[Mage.exe（清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)|对于 Visual Basic，视觉对象中生成应用程序和部署清单C#，并且 VisualC++应用程序。<br /><br /> 签名和重新签名的应用程序和部署清单。<br /><br /> 可以从批处理脚本和命令提示符下运行。|  
|[MageUI.exe（图形化客户端中的清单生成和编辑工具）](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)|生成和编辑应用程序和部署清单。<br /><br /> 签名和重新签名的应用程序和部署清单。|  
|[GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)|生成应用程序清单。<br /><br /> 可以从 MSBuild 运行。 有关详细信息，请参阅 [MSBuild 参考](../msbuild/msbuild-reference.md)。|  
|[GenerateDeploymentManifest 任务](../msbuild/generatedeploymentmanifest-task.md)|生成部署清单。<br /><br /> 可以从 MSBuild 运行。 有关详细信息，请参阅 [MSBuild 参考](../msbuild/msbuild-reference.md)。|  
|[SignFile 任务](../msbuild/signfile-task.md)|登录应用程序和部署清单。<br /><br /> 可以从 MSBuild 运行。 有关详细信息，请参阅 [MSBuild 参考](../msbuild/msbuild-reference.md)。|  
|<xref:Microsoft.Build.Tasks.Deployment.ManifestUtilities>|开发您自己的应用程序，以生成应用程序和部署清单。|  
  
 下表显示了支持以下浏览器中的 ClickOnce 应用程序所需的.NET Framework 版本。  
  
|浏览者|.NET Framework 版本|  
|-------------|----------------------------|  
|Internet Explorer|2.0、3.0、3.5、3.5 SP1、4|  
|Firefox|2.0 SP1、3.5 SP1、4|  
  
## <a name="see-also"></a>请参阅  
 [在 Windows Vista 上的 ClickOnce 部署](../deployment/clickonce-deployment-on-windows-vista.md)   
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)   
 [使用 ClickOnce 部署 COM 组件](../deployment/deploying-com-components-with-clickonce.md)   
 [从命令行生成 ClickOnce 应用程序](../deployment/building-clickonce-applications-from-the-command-line.md)   
 [调试使用 System.Deployment.Application 的 ClickOnce 应用程序](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)
