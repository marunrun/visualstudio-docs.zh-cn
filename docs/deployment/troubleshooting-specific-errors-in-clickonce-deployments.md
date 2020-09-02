---
title: ClickOnce 部署中的特定错误疑难解答 |Microsoft Docs
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fac7f18244aaa32667514766ad6d393408997e51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "87235155"
---
# <a name="troubleshoot-specific-errors-in-clickonce-deployments"></a>ClickOnce 部署中特定错误的疑难解答
本文列出了在部署应用程序时可能出现的以下常见错误 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，并提供解决每个问题的步骤。

## <a name="general-errors"></a>常规错误

#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>当你尝试查找应用程序文件时，不会发生任何事情或在 Internet Explorer 中呈现 XML，或者你会收到 "运行" 或 "另存为" 对话框
 此错误可能是由于内容类型 (也称为 MIME 类型) 未在服务器或客户端上正确注册。

 首先，请确保将服务器配置为将 *应用程序* 扩展与内容类型应用程序/x 应用程序相关联。

 如果服务器配置正确，请检查计算机上是否安装了 .NET Framework 2.0。 如果安装了 .NET Framework 2.0，但仍看到此问题，请尝试卸载并重新安装 .NET Framework 2.0，以便在客户端上重新注册内容类型。

#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>错误消息显示 "无法检索应用程序。 部署中缺少文件 "或" 应用程序下载已中断，请检查是否存在网络错误，然后重试 "
 此消息指示无法下载清单引用的一个或多个文件 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 调试此错误的最简单方法是尝试下载 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 无法下载的 URL。 下面是一些可能的原因：

- 如果日志文件显示 " (403) 禁止访问" 或 " (404) 找不到"，则验证是否配置了 Web 服务器，使其不会阻止下载此文件。 有关详细信息，请参阅 [ClickOnce 部署中的服务器和客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)。

- 如果此 *.config* 文件被服务器阻止，请参阅本文后面的 "尝试安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 包含 .config 文件的应用程序时下载错误" 部分。

- 确定此错误是否发生，因为 `deploymentProvider` 部署清单中的 url 指向的位置与用于激活的 url 的位置不同。

- 确保所有文件都存在于服务器上; [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 日志应告诉你找不到哪个文件。

- 查看是否存在网络连接问题;如果客户端计算机在下载过程中处于脱机状态，则可以收到此消息。

#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>尝试安装包含 .config 文件的 ClickOnce 应用程序时出现下载错误
 默认情况下，基于 Windows 的应用程序 Visual Basic 包括 App.config 文件。 当用户尝试从使用 Windows Server 2003 的 Web 服务器进行安装时，将会出现问题，因为出于安全原因，操作系统会阻止安装 *.config* 文件。 若要启用要安装的 *.config*文件，请单击 "**发布选项**" 对话框中的 **"使用部署" 文件扩展名**。

 还必须将内容类型 (也称为 MIME 类型）设置为适用于. application、.manifest 和 .deploy 文件) 。 有关详细信息，请参阅 Web 服务器文档。

 有关详细信息，请参阅 [ClickOnce 部署中的服务器和客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)中的 "Windows Server 2003：锁定的内容类型"。

#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>错误消息： "应用程序的格式不正确;"日志文件包含 "XML 签名无效"
 确保已更新清单文件并再次对其进行签名。 使用重新发布应用程序， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 或使用 Mage 再次对应用程序进行签名。

#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>你在服务器上更新了应用程序，但客户端未下载更新
 通过完成以下任务之一，可以解决此问题：

- 检查 `deploymentProvider` 部署清单中的 URL。 确保正在更新指向的同一位置中的位 `deploymentProvider` 。

- 验证部署清单中的更新间隔。 如果此时间间隔设置为定期间隔（例如每六个小时一次）， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 则在此间隔结束之前，将不会扫描更新。 你可以更改清单，以便在每次应用程序启动时扫描更新。 在开发时，更改更新间隔是一个方便的选项，用于验证正在安装的更新，但这会降低应用程序激活的速度。

- 尝试再次在 "开始" 菜单上启动该应用程序。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可能已在后台检测到更新，但会提示你在下一次激活时安装 bits。

#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>在更新过程中，你将收到一个错误，其中包含以下日志条目： "部署中的引用与应用程序清单中定义的标识不匹配"
 发生此错误的原因可能是您已手动编辑了部署和应用程序清单，并导致一个清单中的程序集标识的说明与其他清单不同步。 程序集的标识由其名称、版本、区域性和公钥标记组成。 检查清单中的标识说明，并更正所有差异。

#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>第一次从本地磁盘或 cd-rom 激活时，它会成功，但从 "开始" 菜单后续激活并不成功
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用部署提供程序 URL 接收应用程序的更新。 验证 URL 指向的位置是否正确。

#### <a name="error-cannot-start-the-application"></a>错误： "无法启动应用程序"
 此错误消息通常表示将此应用程序安装到存储区时出现问题 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 应用程序错误或存储已损坏。 日志文件可能会告诉您错误发生的位置。

 你应执行以下操作：

- 验证部署清单的标识、应用程序清单的标识和主应用程序 EXE 的标识是否都是唯一的。

- 验证文件路径的长度不超过100个字符。 如果你的应用程序包含太长的文件路径，则可能会超出你可存储的最大路径的限制。 请尝试缩短路径，然后重新安装。

#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>不遵守应用程序配置文件中的 PrivatePath 设置
 若要使用 PrivatePath (合成探测路径) ，应用程序必须请求完全信任权限。 尝试将应用程序清单更改为请求完全信任，然后重试。

#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>在卸载过程中，会显示一条消息，指出 "未能卸载应用程序"
 此消息通常表示应用程序已删除或存储已损坏。 单击 **"确定**" 后，将删除 " **添加/删除程序** " 项。

#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>在安装过程中，会出现一条消息，指出未安装平台依赖项
 GAC (全局程序集缓存中缺少一个必备组件) 应用程序需要该程序才能运行。

## <a name="publishing-with-visual-studio"></a>通过 Visual Studio 进行发布

#### <a name="publishing-in-visual-studio-fails"></a>在 Visual Studio 中发布失败
 确保你有权发布到目标服务器。 例如，如果你以普通用户（而不是管理员）身份登录到终端服务器计算机，则你可能不具有发布到本地 Web 服务器所需的权限。

 如果你使用 URL 发布，请确保目标计算机已启用 FrontPage 服务器扩展。

#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>错误消息：无法创建网站 " \<site> "。 未安装用于与 FrontPage 服务器扩展通信的组件。
 请确保在要发布的计算机上安装了 Microsoft Visual Studio Web 创作组件。 对于 Express 用户，默认情况下不安装此组件。 有关详细信息，请参阅 [http://go.microsoft.com/fwlink/?LinkId=102310](https://support.microsoft.com/help/945358)。

#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>错误消息：找不到文件 "6.0.0.0，Version =，Culture = *，PublicKeyToken = 6595b64144ccf1df，ProcessorArchitecture = \* ，Type = win32"
 当你尝试发布启用了视觉样式的 WPF 应用程序时，会出现此错误消息。 若要解决此问题，请参阅 [如何：发布启用了视觉样式的 WPF 应用程序](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)。

## <a name="using-mage"></a>使用 Mage

#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>尝试使用证书存储区中的证书进行签名，并收到一个空消息框
 在 " **签名** " 对话框中，您必须：

- 选择 " **使用存储的证书签名**"，然后

- 从列表中选择一个证书;第一个证书不是默认选项。

#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>单击 "不签名" 按钮会引发异常
 此问题是已知的 bug。 所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单都需要签名。 只需选择一个签名选项，然后单击 **"确定"**。

## <a name="additional-errors"></a>其他错误
 下表显示了客户端计算机用户在安装应用程序时可能会收到的一些常见错误消息 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 每个错误消息都列在错误的最可能原因的说明旁。

| 错误消息 | 说明 |
| - | - |
| 无法启动应用程序。 请与应用程序发布者联系。<br /><br /> 无法启动应用程序。 请与应用程序供应商联系以获得帮助。 | 这是在无法启动应用程序时出现的一般错误消息，并且找不到其他特定的原因。 通常，这意味着应用程序已损坏或 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 存储已损坏。 |
| 无法继续。 应用程序的格式不正确。 请与应用程序发布者联系以获得帮助。<br /><br /> 应用程序验证失败。 无法继续。<br /><br /> 无法检索应用程序文件。 文件在部署中已损坏。 | 部署中的清单文件之一在语法上无效，或者包含无法与相应文件协调的哈希值。 此错误还可能指示嵌入到程序集内的清单已损坏。 重新创建部署并重新编译应用程序，或在清单中手动查找并修复错误。 |
| 无法检索应用程序。 身份验证错误。<br /><br /> 应用程序安装未成功。 在服务器上找不到应用程序文件。 请与应用程序发布者或管理员联系以获得帮助。 | 无法下载部署中的一个或多个文件，因为您没有访问它们的权限。 这可能是由 Web 服务器返回403禁止的错误引起的，如果部署中的某个文件以使 Web 服务器将其视为受保护的文件的扩展名结束，则可能会出现这种错误。 此外，包含一个或多个应用程序文件的目录可能需要用户名和密码才能访问。 |
| 无法下载该应用程序。 应用程序缺少所需的文件。 请与应用程序供应商或系统管理员联系以获得帮助。 | 在服务器上找不到应用程序清单中列出的一个或多个文件。 检查是否已上传了所有部署的依赖文件，然后重试。 |
| 应用程序下载未成功。 请检查你的网络连接，或者与你的系统管理员或网络服务提供商联系。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 无法建立到服务器的网络连接。 检查服务器的可用性和网络的状态。 |
| URLDownloadToCacheFile 失败，HRESULT 为 " \<number> "。 尝试下载 "" 时出错 \<file> 。 | 如果在部署目标计算机上，用户已将 Internet Explorer 高级安全选项 "在安全和非安全模式之间更改" 设置为 "警告"，并且如果要安装的 ClickOnce 应用程序的安装 URL 从不安全站点重定向到安全站点 (或反之亦然) ，则安装将会失败，因为 Internet Explorer 警告会将其中断。<br /><br /> 若要解决此错误，您可以执行以下任务之一：<br /><br /> -清除 "安全" 选项。<br />-确保未以更改安全模式的方式重定向安装 URL。<br />-完全删除重定向，并指向实际的安装 URL。 |
| 写入硬盘时发生错误。 磁盘上的可用空间可能不足。 请与应用程序供应商或系统管理员联系以获得帮助。 | 这可能表示存储应用程序所用的磁盘空间不足，但当你尝试将应用程序文件保存到驱动器时，它还可能指示更常见的 i/o 错误。 |
| 无法启动应用程序。 磁盘上没有足够的可用空间。 | 硬盘已满。 清除 "空间"，然后尝试再次运行该应用程序。 |
| 部署太多的激活尝试同时加载。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 限制可同时启动的不同应用程序的数目。 这在很大程度上是为了防止恶意尝试对本地服务进行制定的拒绝服务攻击 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ; 尝试定期启动同一个应用程序的用户只会得到一个应用程序实例。 |
| 快捷方式无法通过网络激活。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]只能在本地硬盘上启动应用程序的快捷方式。 无法通过打开指向远程服务器上的快捷方式文件的 URL 来启动它们。 |
| 应用程序太大，无法在部分信任环境中联机运行。 请与应用程序供应商或系统管理员联系以获得帮助。 | 在部分信任环境中运行的应用程序不能大于联机应用程序配额大小的一半，默认值为 250 MB。 |

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)