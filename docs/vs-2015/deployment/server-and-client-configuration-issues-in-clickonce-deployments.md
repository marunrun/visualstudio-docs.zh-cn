---
title: ClickOnce 部署中的服务器和客户端配置问题 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- Windows applications, ClickOnce deployments
ms.assetid: 929e5fcc-dd56-409c-bb57-00bd9549b20b
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5a78fab1986c7fae50bbb4c8149e8f2c89ec4873
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295204"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 部署中的服务器和客户端配置问题
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你在 Windows Server 上使用 Internet Information Services （IIS），并且你的部署包含 Windows 无法识别的文件类型（如 Microsoft Word 文件），则 IIS 将拒绝传输该文件，并且你的部署将不会成功。  
  
 此外，某些 Web 服务器和 Web 应用程序软件（如 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]）包含无法下载的文件和文件类型的列表。 例如，[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 阻止下载所有 web.config 文件。 这些文件可能包含敏感信息，例如用户名和密码。  
  
 尽管此限制对于下载核心 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 文件（如清单和程序集）没有问题，但这种限制可能会阻止你下载作为 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序一部分包含的数据文件。 在 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]中，可以通过删除禁止从 IIS 配置管理器下载此类文件的处理程序来解决此错误。 请参阅 IIS 服务器文档了解更多详细信息。  
  
 某些 Web 服务器可能会阻止扩展名为 .dll、.config 和 .mdf 的文件。 基于 Windows 的应用程序通常包含具有其中一些扩展的文件。 如果用户尝试运行的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序访问 Web 服务器上的被阻止文件，则会产生错误。 默认情况下，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 发布每个具有 ".deploy" 文件扩展名的应用程序文件，而不是取消阻止所有文件扩展名。 因此，管理员只需将 Web 服务器配置为取消阻止以下三个文件扩展名：  
  
- .application  
  
- .manifest  
  
- .deploy  
  
  但是，你可以通过清除 "[发布选项" 对话框](https://msdn.microsoft.com/fd9baa1b-7311-4f9e-8ffb-ae50cf110592)中的 **"使用 ' .deploy ' 文件扩展名**" 选项来禁用此选项，在这种情况下，你必须将 Web 服务器配置为取消阻止应用程序中使用的所有文件扩展名。  
  
  例如，如果使用的是未安装 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]的 IIS，或者使用的是其他 Web 服务器（例如 Apache），则必须配置 .manifest、. application 和 .deploy。  
  
## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce 和安全套接字层（SSL）  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序将通过 SSL 正常工作，除非 Internet Explorer 引发有关 SSL 证书的提示。 当证书出现问题时，可能会引发提示，例如，当站点名称不匹配或证书已过期时。 若要使 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 通过 SSL 连接工作，请确保证书是最新的，并且证书数据与站点数据匹配。  
  
## <a name="clickonce-and-proxy-authentication"></a>ClickOnce 和代理身份验证  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 在 .NET Framework 3.5 中开始提供对 Windows 集成代理身份验证的支持。 不需要特定的 machine.config 指令。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 不支持其他身份验证协议，如 Basic 或 Digest。  
  
 你还可以将修补程序应用到 .NET Framework 2.0 来启用此功能。 有关详细信息，请参阅 https://go.microsoft.com/fwlink/?LinkId=158730。  
  
 有关详细信息，请参阅[\<defaultProxy > 元素（网络设置）](https://msdn.microsoft.com/library/9d663c4b-07b4-4f6f-9b12-efbd3630354f)。  
  
## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce 和 Web 浏览器兼容性  
 目前，只有在使用 Internet Explorer 打开部署清单的 URL 时，才会启动 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 安装。 只有在将 Internet Explorer 设置为默认 Web 浏览器的情况下，从其他应用程序（例如 Microsoft Office Outlook）启动其 URL 的部署才会成功启动。  
  
> [!NOTE]
> 如果部署提供程序不为空或者已安装 Microsoft .NET Framework 助手扩展，则支持 Mozilla Firefox。 此扩展与 .NET Framework 3.5 SP1 一起打包。 对于 XBAP 支持，NPWPF 插件将在需要时激活。  
  
## <a name="activating-clickonce-applications-through-browser-scripting"></a>通过浏览器脚本激活 ClickOnce 应用程序  
 如果您开发了一个使用活动脚本启动 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序的自定义网页，则您可能会发现该应用程序将不会在某些计算机上启动。 Internet Explorer 包含一个称为 "**自动提示文件下载**" 的设置，这会影响此行为。 此设置在其 "**选项**" 菜单中的 "**安全**" 选项卡上可影响此行为。 它被称为**自动提示进行文件下载**，并在 "**下载**" 类别下面列出。 默认情况下，此属性设置为 "为 intranet Web pages**启用**"，默认情况下为 "默认**禁用**"。 如果此设置设置为 "**禁用**"，则将阻止以编程方式激活 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序的任何尝试（例如，通过将其 URL 分配给 `document.location` 属性）。 在这种情况下，用户只能通过用户启动的下载来启动应用程序，例如，通过单击超链接设置为应用程序的 URL。  
  
## <a name="additional-server-configuration-issues"></a>其他服务器配置问题  
  
##### <a name="administrator-permissions-required"></a>需要管理员权限  
 如果要使用 HTTP 进行发布，则必须在目标服务器上具有管理员权限。 IIS 需要此权限级别。 如果不是使用 HTTP 发布，则只需要对目标路径具有写入权限。  
  
##### <a name="server-authentication-issues"></a>服务器身份验证问题  
 当您发布到禁用了 "匿名访问" 的远程服务器时，您将收到以下警告：  
  
```  
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."  
```  
  
> [!NOTE]
> 如果站点提示输入默认凭据以外的凭据，则可以使 NTLM （NT 质询-响应）身份验证正常工作，当系统提示你是否要保存提供的凭据以供将来的会话时，你可以在 "安全" 对话框中单击 **"确定"** 。 但是，此解决方法不适用于基本身份验证。  
  
## <a name="using-third-party-web-servers"></a>使用第三方 Web 服务器  
 如果要从 IIS 之外的 Web 服务器部署 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序，则如果服务器返回密钥 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 文件（如部署清单和应用程序清单）的错误内容类型，则可能会遇到问题。 若要解决此问题，请参阅 Web 服务器的帮助文档，了解如何向服务器添加新内容类型，并确保下表中列出的所有文件扩展名映射都已准备就绪。  
  
|文件扩展名|内容类型|  
|-------------------------|------------------|  
|`.application`|`application/x-ms-application`|  
|`.manifest`|`application/x-ms-manifest`|  
|`.deploy`|`application/octet-stream`|  
|`.msu`|`application/octet-stream`|  
|`.msp`|`application/octet-stream`|  
  
## <a name="clickonce-and-mapped-drives"></a>ClickOnce 和映射驱动器  
 如果使用 Visual Studio 发布 ClickOnce 应用程序，则不能将映射驱动器指定为安装位置。 但是，可以使用清单生成器和编辑器（Mage.exe 和 Mageui.exe）修改 ClickOnce 应用程序，以便从映射的驱动器进行安装。 有关详细信息，请参阅[Mage.exe （清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)并[MageUI.exe（图形化客户端中的清单生成和编辑工具）](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)。  
  
## <a name="ftp-protocol-not-supported-for-installing-applications"></a>用于安装应用程序的 FTP 协议不受支持  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 支持从任何 HTTP 1.1 Web 服务器或文件服务器安装应用程序。 安装应用程序不支持 FTP、文件传输协议。 仅可使用 FTP 发布应用程序。 下表总结了这些差异：  
  
|URL 类型|描述|  
|--------------|-----------------|  
|ftp://|你可以使用此协议发布 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。|  
|http://|你可以使用此协议安装 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。|  
|https://|你可以使用此协议安装 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。|  
|file://|你可以使用此协议安装 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。|  
  
## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2： Windows 防火墙  
 默认情况下，Windows XP SP2 启用 Windows 防火墙。 如果要在安装了 Windows XP 的计算机上开发应用程序，仍可以从运行 IIS 的本地服务器发布和运行 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。 但是，除非打开 Windows 防火墙，否则不能从另一台计算机访问运行 IIS 的服务器。 有关管理 Windows 防火墙的说明，请参阅 Windows 帮助。  
  
## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server：启用 FrontPage 服务器扩展  
 若要将应用程序发布到使用 HTTP 的 Windows Web 服务器，则需要 Microsoft 提供的 FrontPage 服务器扩展。  
  
 默认情况下，Windows Server 未安装 FrontPage 服务器扩展。 如果要使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 发布到使用 HTTP 与 FrontPage 服务器扩展的 Windows Server Web 服务器，则必须先安装 FrontPage 服务器扩展。 您可以使用 Windows Server 中的 "管理您的服务器管理工具" 执行安装。  
  
## <a name="windows-server-locked-down-content-types"></a>Windows Server：锁定的内容类型  
 [!INCLUDE[WinXPSvr](../includes/winxpsvr-md.md)] 上的 IIS 会锁定除某些已知内容类型之外的所有文件类型（例如，.htm、.html、.txt，等等）。 若要使用此服务器启用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序的部署，你需要更改 IIS 设置，以允许下载类型为. application、.manifest 的文件和应用程序使用的任何其他自定义文件类型。  
  
 如果使用 IIS 服务器进行部署，请运行 inetmgr 并为默认网页添加新的文件类型：  
  
- 对于应用程序和清单扩展，MIME 类型应为 "应用程序/x 应用程序"。 对于其他文件类型，MIME 类型应为 "application/八进制流"。  
  
- 如果创建扩展名为 "*" 且 MIME 类型为 "application/八进制流" 的 MIME 类型，则将允许下载不受阻止的文件类型的文件。 （但是，不能下载被阻止的文件类型，如 .aspx 和 .asmx。）  
  
  有关在 Windows Server 上配置 MIME 类型的具体说明，请参阅 Microsoft 知识库文章 KB326965 "IIS 6.0 不提供未知 MIME 类型" [https://support.microsoft.com/default.aspx?scid=kb; en-us; 326965](https://support.microsoft.com/default.aspx?scid=kb;en-us;326965)。  
  
## <a name="content-type-mappings"></a>内容类型映射  
 通过 HTTP 发布时，应用程序文件的内容类型（也称为 MIME 类型）应为 "应用程序/x 应用程序"。 如果已在服务器上安装 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]，则会自动设置。 如果未安装，则需要为 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序 vroot （或整个服务器）创建 MIME 类型关联。  
  
 如果使用 IIS 服务器进行部署，请运行 inetmgr，并为应用程序扩展添加新的 "应用程序/x 应用程序" 内容类型。  
  
## <a name="http-compression-issues"></a>HTTP 压缩问题  
 使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]，你可以执行使用 HTTP 压缩的下载，它是使用 GZIP 算法在将流发送到客户端之前压缩数据流的 Web 服务器技术。 在这种情况下，客户端（在本例中为 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]）将在读取文件之前对其进行解压缩。  
  
 如果使用的是 IIS，则可以轻松启用 HTTP 压缩。 但是，当启用 HTTP 压缩时，仅对某些文件类型（即 HTML 和文本文件）启用它。 若要为程序集（.dll）、XML （.xml）、部署清单（应用程序）和应用程序清单（.manifest）启用压缩，则必须将这些文件类型添加到 IIS 的类型列表中以进行压缩。 将文件类型添加到部署之前，只会压缩文本和 HTML 文件。  
  
 有关 IIS 的详细说明，请参阅[如何为 HTTP 压缩指定其他文档类型](https://go.microsoft.com/fwlink/?LinkId=178459)。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)   
 [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
