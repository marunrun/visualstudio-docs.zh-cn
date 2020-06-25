---
title: ClickOnce 安全和部署 |Microsoft Docs
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d33e99d11007ca4684f3d875620e2baeb7ddc1e7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285489"
---
# <a name="clickonce-security-and-deployment"></a>ClickOnce 安全性和部署
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]是一项部署技术，使你能够创建基于 Windows 的自我更新应用程序，这些应用程序可以通过最少的用户交互进行安装和运行。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]如果已使用 Visual Basic 和 Visual c # 开发了项目，则对发布和更新使用 ClickOnce 技术部署的应用程序提供完全支持。 有关部署 Visual C++ 应用程序的信息，请参阅[Visual C++ 应用程序的 ClickOnce 部署](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署克服了部署中的三个主要问题：

- **更新应用程序时遇到困难。** 使用 Microsoft Windows Installer 部署，每当更新应用程序时，用户都可以安装更新和 msp 文件，并将其应用于已安装的产品;通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署，你可以自动提供更新。 只会下载应用程序中已更改的部分，然后从新的并行文件夹重新安装完整的、更新的应用程序。

- **对用户计算机的影响。** 利用 Windows Installer 部署，应用程序通常依赖于共享组件，可能会导致版本控制冲突;对于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署，每个应用程序都是独立的，不能干扰其他应用程序。

- **安全权限。** Windows Installer 部署需要管理权限，并且仅允许受限用户安装;[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署使非管理用户能够仅安装和授予应用程序所需的代码访问安全权限。

  过去，这些问题有时会导致开发人员决定创建 Web 应用程序而不是基于 Windows 的应用程序，从而牺牲了丰富的用户界面以便于安装。 通过使用通过部署的应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，你可以获得这两种技术的优势。

## <a name="what-is-a-clickonce-application"></a>什么是 ClickOnce 应用程序？
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序是使用技术发布的任何 Windows Presentation Foundation （*xbap*）、Windows 窗体（*.exe*）、控制台应用程序（.dll）或 Office 解决方案（*.dll*）*.exe* [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 通过三种不同的方式发布应用程序：从网页、从网络文件共享或从媒体（如 cd-rom）。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序可以安装在最终用户的计算机上，甚至在计算机脱机时也可以在本地运行，也可以仅在联机模式下运行，而无需在最终用户的计算机上永久安装任何内容。 有关详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序可以自我更新;他们可以检查是否有更新的版本，并自动替换所有更新的文件。 开发人员可以指定更新行为；网络管理员也可以控制更新策略，如将更新标记为强制性更新。 最终用户或管理员还可以将更新回滚到早期版本。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 由于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是独立的，因此安装或运行 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序不能中断现有的应用程序。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序是独立的;每个应用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 程序都安装到安全的每个用户、每个应用程序缓存中并运行。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序在 Internet 或 Intranet 安全区域中运行。 必要时，应用程序可以请求提升的安全权限。 有关详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

## <a name="how-clickonce-security-works"></a>ClickOnce 安全的工作原理
 核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安全基于证书、代码访问安全策略和 ClickOnce 信任提示。

### <a name="certificates"></a>证书
 Authenticode 证书用于验证应用程序发行者的真实性。 通过对应用程序部署使用 Authenticode，ClickOnce 有助于防止有害程序描绘自身作为来自已建立的可信源的合法程序。 另外，还可以使用证书对应用程序和部署清单进行签名，以证明文件未被篡改。 有关详细信息，请参阅[ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)。 证书还可用于将客户端计算机配置为具有受信任的发布者列表。 如果某个应用程序来自受信任的发布者，则可以在不进行任何用户交互的情况下进行安装。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

### <a name="code-access-security"></a>代码访问安全性
 代码访问安全性有助于限制代码对受保护资源的访问权限。 在大多数情况下，你可以选择 "Internet" 或 "本地 Intranet" 区域来限制权限。 使用**ProjectDesigner**中的 "**安全**" 页来请求适用于该应用程序的区域。 你还可以调试具有受限权限的应用程序，以模拟最终用户体验。 有关详细信息，请参阅[ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)。

### <a name="clickonce-trust-prompt"></a>ClickOnce 信任提示
 如果应用程序请求的权限超过区域允许的权限，则系统会提示最终用户进行信任决定。 最终用户可以决定 ClickOnce 应用程序（如 Windows 窗体应用程序、Windows Presentation Foundation 应用程序、控制台应用程序、XAML 浏览器应用程序和 Office 解决方案）是否受信任才能运行。 有关详细信息，请参阅[如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。

## <a name="how-clickonce-deployment-works"></a>ClickOnce 部署的工作原理
 核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署体系结构基于以下两个 XML 清单文件：应用程序清单和部署清单。 文件用于描述 ClickOnce 应用程序的安装位置、更新方式以及更新时间。

### <a name="publish-clickonce-applications"></a>发布 ClickOnce 应用程序
 应用程序清单描述应用程序本身。 这包括程序集、构成应用程序的依赖项和文件、所需的权限以及可用更新的位置。 应用程序开发人员通过使用 Visual Studio 中的 "发布向导" 或中的清单生成和编辑工具（*Mage.exe*）来创作应用程序清单 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

 部署清单描述应用程序的部署方式。 这包括应用程序清单的位置和客户端应运行的应用程序的版本。

### <a name="deploy-clickonce-applications"></a>部署 ClickOnce 应用程序
 创建后，会将部署清单复制到部署位置。 该位置可以是 Web 服务器、网络文件共享或媒体（如 CD）。 应用程序清单和所有应用程序文件也会复制到部署清单中指定的部署位置。 该位置可以与部署清单的部署位置相同，也可以不同。 在 Visual Studio 中使用**发布向导**时，会自动执行复制操作。

### <a name="install-clickonce-applications"></a>安装 ClickOnce 应用程序
 在将其部署到部署位置后，最终用户可以通过单击代表网页或文件夹中的部署清单文件的图标来下载和安装应用程序。 在大多数情况下，最终用户会看到一个简单的对话框，要求用户确认安装，之后安装会继续，并且应用程序在无需额外干预的情况下启动。 在应用程序需要提升权限的情况下，或者如果应用程序未使用受信任的证书进行签名，则对话框还会要求用户授予权限，然后才能继续安装。 尽管 ClickOnce 安装按用户进行，但如果存在需要管理员权限的先决条件，则可能需要权限提升。 有关提升权限的详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

 可以在计算机或企业级别信任证书，以便使用受信任证书签名的 ClickOnce 应用程序可以无提示方式进行安装。 有关受信任证书的详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

 可将应用程序添加到用户的 "**开始**" 菜单和 "**控制面板**" 的 "**添加或删除程序**" 组。 不同于其他部署技术，不会将任何内容添加到**Program Files**文件夹或注册表，并且无需管理权限即可安装

> [!NOTE]
> 还可以阻止将应用程序添加到 "**开始**" 菜单和 "**添加或删除程序**" 组，这实际上会使其行为类似于 Web 应用程序。 有关详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

### <a name="update-clickonce-applications"></a>更新 ClickOnce 应用程序
 当应用程序开发人员创建应用程序的更新版本时，它们会生成新的应用程序清单，并将文件复制到部署位置，通常是原始应用程序部署文件夹的同级文件夹。 管理员更新部署清单，使其指向新版本的应用程序的位置。

> [!NOTE]
> 可以使用 Visual Studio 中的 "**发布向导**" 来执行这些步骤。

 除了部署位置，部署清单还包含一个更新位置（一个网页或网络文件共享），应用程序将在其中检查更新的版本。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]**发布**属性用于指定应用程序检查更新的时间和频率。 可以在部署清单中指定更新行为，也可以通过 api 将其显示为应用程序用户界面中的用户选择 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此外，Publish 属性还可用于将更新设置为强制执行，或用于将应用程序回滚到较早版本****。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

### <a name="third-party-installers"></a>第三方安装程序
 您可以自定义 ClickOnce 安装程序，以便与您的应用程序一起安装第三方组件。 你必须具有可再发行组件包（.exe 或 .msi 文件），并使用特定于语言的产品清单和特定于语言的包清单描述包。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

## <a name="clickonce-tools"></a>ClickOnce 工具
 下表显示了可用于对应用程序和部署清单进行生成、编辑、签名和重新签名的工具。

|工具|说明|
|----------|-----------------|
|[”项目设计器“ -&gt;“安全”页](../ide/reference/security-page-project-designer.md)|对应用程序和部署清单进行签名。|
|[发布页，项目设计器](../ide/reference/publish-page-project-designer.md)|为 Visual Basic 和 Visual c # 应用程序生成和编辑应用程序和部署清单。|
|[*Mage.exe* （清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)|为 Visual Basic、Visual c # 和 Visual C++ 应用程序生成应用程序和部署清单。<br /><br /> 对应用程序和部署清单进行签名和重新签名。<br /><br /> 可以从批处理脚本和命令提示符运行。|
|[*MageUI.exe* （清单生成和编辑工具，图形客户端）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)|生成和编辑应用程序和部署清单。<br /><br /> 对应用程序和部署清单进行签名和重新签名。|
|[GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)|生成应用程序清单。<br /><br /> 可从 MSBuild 运行。 有关详细信息，请参阅[MSBuild reference](../msbuild/msbuild-reference.md)。|
|[GenerateDeploymentManifest 任务](../msbuild/generatedeploymentmanifest-task.md)|生成部署清单。<br /><br /> 可从 MSBuild 运行。 有关详细信息，请参阅[MSBuild reference](../msbuild/msbuild-reference.md)。|
|[SignFile 任务](../msbuild/signfile-task.md)|对应用程序和部署清单进行签名。<br /><br /> 可从 MSBuild 运行。 有关详细信息，请参阅[MSBuild reference](../msbuild/msbuild-reference.md)。|
|[Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/microsoft.build.tasks.deployment.manifestutilities)|开发自己的应用程序来生成应用程序清单和部署清单。|

 下表显示了在这些浏览器中支持 ClickOnce 应用程序所需的 .NET Framework 版本。

|浏览者|.NET Framework 版本|
|-------------|----------------------------|
|Internet Explorer|2.0、3.0、3.5、3.5 SP1、4|
|Firefox|2.0 SP1、3.5 SP1、4|
|Chrome|3.5|
|Microsoft Edge|3.5|

## <a name="see-also"></a>另请参阅
- [Windows Vista 上的 ClickOnce 部署](../deployment/clickonce-deployment-on-windows-vista.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [使用 ClickOnce 部署 COM 组件](../deployment/deploying-com-components-with-clickonce.md)
- [从命令行生成 ClickOnce 应用程序](../deployment/building-clickonce-applications-from-the-command-line.md)
- [调试使用 System.web 的 ClickOnce 应用程序](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)
