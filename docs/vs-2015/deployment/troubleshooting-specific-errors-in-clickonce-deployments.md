---
title: ClickOnce 部署中的特定错误的疑难解答 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: troubleshooting
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.UncRequired
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.NoInstallUrl
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
ms.assetid: 22dfe8f1-8271-4708-9c25-6bbb13920ac8
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 348cb15ebc348d6c0ece5e7118e896cc6a21b23b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62420133"
---
# <a name="troubleshooting-specific-errors-in-clickonce-deployments"></a>ClickOnce 部署中的特定错误的疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题列出了在部署时可能发生的以下常见错误[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序，并提供了步骤来解决每个问题。  
  
## <a name="general-errors"></a>常规错误  
  
#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>当你尝试寻找.application 文件，没有出现任何问题，或 XML 呈现在 Internet Explorer 中，或收到一个运行或另存为对话框  
 未在服务器或客户端上正确注册内容类型 （也称为 MIME 类型） 可能导致此错误。  
  
 首先，请确保将服务器配置为将.application 扩展名与"应用程序/x 的 ms-应用程序"的内容类型相关联。  
  
 如果将服务器配置正确，请确保[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]在计算机上安装。 如果[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]已安装，并且你仍看到此问题，请尝试卸载并重新安装[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]重新注册客户端上的内容类型。  
  
#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>错误消息指出，"无法检索应用程序。 在部署中缺少的文件"或"应用程序下载已中断、 检查网络错误中并稍后重试"  
 此消息表示所引用的一个或多个文件[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]无法下载的清单。 若要调试此错误的最简单方法是尝试下载该 URL 的[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]说不能下载。 下面是一些可能的原因：  
  
- 如果日志文件说"(403) 禁止访问"或"(404) 找不到，"验证配置 Web 服务器，以便它不会阻止下载此文件。 有关详细信息，请参阅 [ClickOnce 部署中的服务器和客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)。  
  
- 如果在服务器被阻止的.config 文件，请参阅"下载错误，当您尝试安装[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]具有.config 文件的应用程序"本主题中更高版本。  
  
- 确定是否发生这种情况`deploymentProvider`部署清单中的 URL 指向用于激活的 URL 不同的位置。  
  
- 确保所有文件都均存在于服务器;[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]日志应告诉您找不到的文件。  
  
- 查看是否存在网络连接问题;如果客户端计算机在下载期间脱机，会收到此消息。  
  
#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>当您尝试安装的 ClickOnce 应用程序.config 文件下载错误  
 默认情况下，Visual Basic Windows 基于应用程序包括一个 App.config 文件。 当用户尝试从使用 Windows Server 2003 的 Web 服务器安装，因为该操作系统会阻止出于安全原因的.config 文件的安装时将有问题。 若要启用要安装的.config 文件，请单击**使用".deploy"文件扩展名**中**发布选项**对话框。  
  
 您还必须设置内容类型 （也称为 MIME 类型） 适当地为.application、.manifest 和.deploy 文件。 有关详细信息，请参阅您的 Web 服务器文档。  
  
 有关详细信息，请参阅"Windows Server 2003:锁定的内容类型"[服务器和 ClickOnce 部署中的客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)。  
  
#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>错误消息："应用程序格式不正确";日志文件包含"XML 签名无效"  
 请确保你已更新的清单文件且再次对它签名。 通过使用重新发布应用程序[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]或使用 Mage 应用程序再次进行签名。  
  
#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>更新应用程序的服务器上，但客户端不会下载更新  
 通过完成以下任务之一，可能会解决此问题：  
  
- 检查`deploymentProvider`部署清单中的 URL。 确保要更新的同一位置中的位的`deploymentProvider`指向。  
  
- 验证部署清单中的更新间隔。 如果在此间隔设置为定期间隔，如每六个小时，一次[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]将不会扫描更新之前已超过此间隔。 您可以更改要扫描每次启动应用程序的更新的清单。 更改的更新间隔是在开发期间一个方便的选项来验证正在安装更新，但会降低应用程序激活。  
  
- 请尝试重新启动该应用程序，在开始菜单上。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 可能已在后台，检测到更新，但将提示你在下一次激活上安装 bits。  
  
#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>在更新期间你收到的错误的以下日志条目："部署中的引用与应用程序清单中定义的标识不匹配"  
 因为您已手动编辑部署和应用程序清单，并导致一个清单，以变得不同步与其他程序集标识的说明，可能会发生此错误。 程序集标识由其名称、 版本、 区域性和公钥标记组成。 检查对清单中的标识描述并更正任何差异。  
  
#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>第一次从本地磁盘或 CD-ROM 激活成功，但从开始菜单的后续激活未成功  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用部署提供程序 URL 来接收应用程序的更新。 验证该 URL 指向的位置正确。  
  
#### <a name="error-cannot-start-the-application"></a>错误："无法启动该应用程序"  
 此错误消息通常表示没有安装到此应用程序时出现问题[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]存储。 应用程序发生错误，或者在存储区已损坏。 日志文件可能会告诉您发生错误的位置。  
  
 您应执行以下操作：  
  
- 验证所有唯一的部署清单的标识、 应用程序清单的标识和主应用程序 EXE 的标识。  
  
- 验证文件路径不超过 100 个字符。 如果你的应用程序包含文件路径太长，则可能会超过路径可以存储的最大限制。 请缩短路径并重新安装。  
  
#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>不遵循应用程序配置文件中的 PrivatePath 设置  
 若要使用 PrivatePath （合成探测路径），该应用程序必须请求完全信任权限。 请尝试更改应用程序清单来请求完全信任，然后重试。  
  
#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>在卸载消息出现，"无法卸载应用程序"  
 此消息通常指示已删除应用程序或存储已损坏。 单击后**确定**，则**添加/删除程序**项将被删除。  
  
#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>在安装期间，出现一条消息指出未安装平台依赖项  
 缺少中 GAC （全局程序集缓存） 的应用程序运行所需的必备组件。  
  
## <a name="publishing-with-visual-studio"></a>使用 Visual Studio 进行发布  
  
#### <a name="publishing-in-visual-studio-fails"></a>在 Visual Studio 中的发布失败  
 确保你有权发布到服务器所面向。 例如，如果登录到终端服务器的计算机作为普通用户，不作为管理员，则您可能没有要发布到本地 Web 服务器所需的权限。  
  
 如果您要发布的 url，请确保目标计算机已启用 FrontPage 服务器扩展。  
  
#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>错误消息：无法创建网站\<站点 >。 未安装与 FrontPage 服务器扩展进行通信的组件。  
 确保您有 Microsoft Visual Studio Web 创作组件从发布在计算机上安装。 对于 Express 用户，默认情况下未安装此组件。 有关详细信息，请参阅 [http://go.microsoft.com/fwlink/?LinkId=102310](http://go.microsoft.com/fwlink/?LinkId=102310)。  
  
#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>错误消息：Could not find file 'Microsoft.Windows.Common-Controls, Version=6.0.0.0, Culture=*, PublicKeyToken=6595b64144ccf1df, ProcessorArchitecture=\*, Type=win32'  
 当你尝试发布启用了视觉样式的 WPF 应用程序时，会出现此错误消息。 若要解决此问题，请参阅[如何：发布启用了视觉样式的 WPF 应用程序](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)。  
  
## <a name="using-mage"></a>使用 Mage  
  
#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>尝试登录时使用你的证书存储和接收到的空消息框中的证书  
 在中**签名**对话框中，您必须：  
  
- 选择**使用存储的证书签名**，和  
  
- 从列表; 选择一个证书第一个证书不是默认选择。  
  
#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>单击"不登录"按钮时导致异常  
 此问题是一个已知的 bug。 所有[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]清单都需要进行签名。 只需选择一个签名的选项，然后依次**确定**。  
  
## <a name="additional-errors"></a>其他错误  
 下表显示了一些常见的错误消息，在用户安装时，可能会收到客户端计算机用户[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 每个错误消息的最可能原因的错误说明旁边列出。  
  
|错误消息|描述|  
|-------------------|-----------------|  
|无法启动应用程序。 请联系应用程序发布者。<br /><br /> 无法启动该应用程序。 与应用程序供应商联系以获得帮助。|这些是无法启动该应用程序，并可在任何其他特定原因时出现一般错误消息。 通常，应用程序以某种方式损坏，这意味着或的[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]存储已损坏。|  
|无法继续。 应用程序的格式不正确。 与应用程序发布者联系以获得帮助。<br /><br /> 应用程序验证未成功。 无法继续。<br /><br /> 无法检索应用程序文件。 部署中已损坏的文件。|在部署中的清单文件之一是语法上无效，或包含不能为与相应的文件进行对帐的哈希。 此错误也可能表示嵌入在程序集中的清单已损坏。 重新创建你的部署和重新编译应用程序，或查找并在清单中手动修复错误。|  
|无法检索应用程序。 身份验证错误。<br /><br /> 应用程序安装未成功。 找不到服务器上的应用程序文件。 与应用程序发布者或管理员联系以获得帮助。|无法下载部署中的一个或多个文件，因为您没有权限访问它们。 原因可能是由 Web 服务器，在部署中的文件之一使 Web 服务器视为受保护的文件扩展名结尾，则可能发生返回 403 禁止访问错误。 此外，包含一个或多个应用程序的文件的目录可能需要用户名和密码才能访问。|  
|无法下载该应用程序。 应用程序缺少所需的文件。 与应用程序供应商或系统管理员联系以获得帮助。|在服务器上找不到一个或多个应用程序清单中列出的文件。 验证你已上载将部署的所有依赖文件，然后重试。|  
|应用程序下载失败。 检查网络连接，或联系你的系统管理员或网络服务提供商。|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 无法建立到服务器的网络连接。 检查服务器的可用性和网络的状态。|  
|URLDownloadToCacheFile 失败，HRESULT\<数 >。 尝试下载时出错\<文件 >。|如果用户已设置 Internet Explorer 高级安全选项"如果之间安全的更改，则发出警告和非安全模式"的部署目标计算机上，并且安装程序正在安装的 ClickOnce 应用程序的重定向 URL 从非安全到安全站点 （或反之亦然），则安装将失败，因为 Internet Explorer 警告会中断它。<br /><br /> 若要解决此问题，可以执行下列任一操作：<br /><br /> -清除安全选项。<br />-请确保安装程序 URL 不会重定向的方式来更改安全模式中。<br />-完全删除的重定向和指向实际的安装程序的 URL。|  
|错误写入到硬盘。 可能有足够的空间可用磁盘上。 与应用程序供应商或系统管理员联系以获得帮助。|这可能表示没有足够的磁盘空间来存储应用程序，但它也可能表示更为通用的 I/O 错误，当你尝试将应用程序文件保存到驱动器。|  
|无法启动该应用程序。 在磁盘上没有足够的可用空间。|硬盘已满。 清理空间，并尝试再次运行应用程序。|  
|过多的已部署的激活尝试加载在一次。|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 可以在同一时间开始的不同应用程序的数量限制。 这主要是为了帮助防止恶意发起拒绝服务攻击尝试针对本地[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]服务; 如果尝试在短期内重复，启动同一应用程序，仅将最终有的单个实例的用户应用程序。|  
|不能通过网络激活快捷方式。|快捷方式[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]只能在本地硬盘上启动应用程序。 它们不能通过打开指向远程服务器上的快捷方式文件的 URL 来启动。|  
|应用程序是太大而无法联机在部分信任环境中运行。 与应用程序供应商或系统管理员联系以获得帮助。|在部分信任环境中运行的应用程序不能大于联机应用程序，配额，它默认为 250 MB 大小的一半。|  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)   
 [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
