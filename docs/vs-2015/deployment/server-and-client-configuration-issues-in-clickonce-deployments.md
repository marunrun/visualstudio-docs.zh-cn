---
title: 服务器和 ClickOnce 部署中的客户端配置问题 |Microsoft Docs
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
ms.openlocfilehash: 8b8f81f22ffe566524e45a62330bc95c8ce00016
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686372"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 部署中的服务器和客户端配置问题
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果在 Windows Server 上使用 Internet 信息服务 (IIS) 和你的部署包含 Windows 无法识别的文件类型，如 Microsoft Word 文件，IIS 将拒绝传输该文件中，并且你的部署将不会成功。  
  
 此外，某些 Web 服务器和 Web 应用程序软件，如[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]、 包含一组文件和文件类型不能下载。 例如，[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]可防止所有 Web.config 文件的下载。 这些文件可能包含敏感信息，如用户名和密码。  
  
 尽管此限制应没有引起问题下载核心[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]文件，如清单和程序集，此限制可能会阻止你下载的一部分提供的数据文件在[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 在[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]，可以通过删除禁止下载 IIS 配置管理器中的此类文件的处理程序来解决此错误。 请参阅其他详细信息的 IIS 服务器文档。  
  
 某些 Web 服务器可能会阻止具有.dll、.config 中和.mdf 等扩展名的文件。 基于 Windows 的应用程序通常包括具有这些扩展名的一些文件。 如果用户尝试运行[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]访问 Web 服务器上被阻止的文件的应用程序，将导致错误。 而不是取消阻止所有文件扩展名，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]默认情况下发布".deploy"文件扩展名为每个应用程序文件。 因此，管理员只需将 Web 服务器配置为允许以下三个文件扩展名：  
  
- .application  
  
- .manifest  
  
- .deploy  
  
  但是，可以禁用此选项通过清除**使用".deploy"文件扩展名**选项卡上[Publish Options Dialog Box](https://msdn.microsoft.com/fd9baa1b-7311-4f9e-8ffb-ae50cf110592)，在这种情况下必须配置 Web 服务器以允许所有文件扩展名在应用程序中使用。  
  
  你将需要配置.manifest、.application 和.deploy，例如，如果使用不具有安装的 IIS [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]，或者如果正在使用另一台 Web 服务器 (例如 Apache)。  
  
## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce 和安全套接字层 (SSL)  
 一个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序可以正常工作通过 SSL，除 Internet Explorer 时引发的 SSL 证书相关提示。 错误的证书，如当站点名称不匹配或证书已过期时，可以引发提示。 若要使[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]工作通过 SSL 连接，请确保该证书是最新的并且证书数据与匹配的站点数据。  
  
## <a name="clickonce-and-proxy-authentication"></a>ClickOnce 和代理身份验证  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 从.NET Framework 3.5 的 Windows 集成代理身份验证提供支持。 没有特定 machine.config 指令是必需的。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 不等基本或摘要式其他身份验证协议提供支持。  
  
 此外可以应用于.NET Framework 2.0，若要启用此功能的修补程序。 有关详细信息，请参阅 http://go.microsoft.com/fwlink/?LinkId=158730。  
  
 有关详细信息，请参阅[ \<defaultProxy > 元素 （网络设置）](https://msdn.microsoft.com/library/9d663c4b-07b4-4f6f-9b12-efbd3630354f)。  
  
## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce 和 Web 浏览器兼容性问题  
 目前，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]仅当使用 Internet Explorer 打开部署清单的 URL，将启动安装。 仅当 Internet Explorer 设置为默认 Web 浏览器，从另一个应用程序，如 Microsoft Office Outlook 启动其 URL，则的部署将成功启动。  
  
> [!NOTE]
> 如果部署提供程序不为空或已安装 Microsoft.NET Framework Assistant 扩展，则支持 Mozilla Firefox。 此扩展与.NET Framework 3.5 SP1 一起打包。 有关 XBAP 支持，在需要时激活插件 NPWPF。  
  
## <a name="activating-clickonce-applications-through-browser-scripting"></a>激活 ClickOnce 应用程序可以通过浏览器脚本  
 如果您已开发一个自定义网页，将启动[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]使用活动脚本应用程序可能会发现在某些计算机上将不启动应用程序。 Internet Explorer 包含名为的设置**自动提示文件下载**，这会影响此行为。 此设置位于**安全**选项卡中其**选项**会影响此行为的菜单。 它称为**文件下载自动提示**，，下列出**下载**类别。 属性设置为**启用**默认情况下，为 intranet Web 页，并向**禁用**默认情况下，Internet Web pages。 如果此设置设置为**禁用**，任何尝试激活[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序以编程方式 (例如，通过将分配到其 URL`document.location`属性) 将被阻止。 在此情况下，用户可以启动应用程序只能通过用户启动的下载，例如，通过单击超链接设置为应用程序的 URL。  
  
## <a name="additional-server-configuration-issues"></a>其他服务器配置问题  
  
##### <a name="administrator-permissions-required"></a>所需的管理员权限  
 如果发布使用 HTTP，必须在目标服务器上具有管理员权限。 IIS 要求此权限级别。 如果您没有将发布使用 HTTP，只需要拥有写入权限的目标路径。  
  
##### <a name="server-authentication-issues"></a>服务器身份验证问题  
 当发布具有"匿名访问"已关闭的远程服务器时，您将收到以下警告：  
  
```  
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."  
```  
  
> [!NOTE]
> 可以让 NTLM （NT 质询-响应） 身份验证工作如果该站点会提示您提供默认凭据，之外的凭据，然后在安全对话框中，单击**确定**如果你想要保存所提供提示你时将来的会话的凭据。 但是，此解决方法将不适用于基本身份验证。  
  
## <a name="using-third-party-web-servers"></a>使用第三方 Web 服务器  
 如果要部署[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]从 Web 服务器 IIS 之外的应用程序，您可能会遇到问题如果服务器返回内容类型不正确的密钥[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]文件，如部署清单和应用程序清单。 若要解决此问题，请参阅有关如何将新内容类型添加到服务器，并确保所有文件名称扩展映射下, 表中都列出的文档位于适当位置的 Web 服务器的帮助。  
  
|文件扩展名|内容类型|  
|-------------------------|------------------|  
|`.application`|`application/x-ms-application`|  
|`.manifest`|`application/x-ms-manifest`|  
|`.deploy`|`application/octet-stream`|  
|`.msu`|`application/octet-stream`|  
|`.msp`|`application/octet-stream`|  
  
## <a name="clickonce-and-mapped-drives"></a>ClickOnce 和映射的驱动器  
 如果使用 Visual Studio 发布 ClickOnce 应用程序，则无法指定映射的驱动器作为安装位置。 但是，可以修改通过使用清单生成器和编辑器 （Mage.exe 和 MageUI.exe） 从映射的驱动器安装 ClickOnce 应用程序。 有关详细信息，请参阅[Mage.exe （清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)并[MageUI.exe（图形化客户端中的清单生成和编辑工具）](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)。  
  
## <a name="ftp-protocol-not-supported-for-installing-applications"></a>FTP 协议不支持用于安装应用程序  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 支持从任何 HTTP 1.1 Web 服务器或文件服务器安装的应用程序。 FTP 文件传输协议不支持用于安装应用程序。 可以使用 FTP 发布应用程序。 下表总结了这些差异：  
  
|URL 类型|描述|  
|--------------|-----------------|  
|ftp://|您可以将发布[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序使用此协议。|  
|http://|你可以安装[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序使用此协议。|  
|https://|你可以安装[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序使用此协议。|  
|file://|你可以安装[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序使用此协议。|  
  
## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2：Windows 防火墙  
 默认情况下，Windows XP SP2 启用 Windows 防火墙。 如果正在开发应用程序在已安装的 Windows XP 的计算机上，您将仍可以发布和运行[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]从正在运行 IIS 的本地服务器的应用程序。 但是，不能访问该服务器正在运行的 IIS 从另一台计算机只有打开 Windows 防火墙。 有关管理 Windows 防火墙的说明，请参阅 Windows 帮助。  
  
## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server：启用 FrontPage 服务器扩展  
 Microsoft FrontPage 服务器扩展是必需的应用程序发布到使用 HTTP 的 Windows Web 服务器。  
  
 默认情况下，Windows Server 没有安装的 FrontPage 服务器扩展。 如果你想要使用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]若要发布到 HTTP 使用 FrontPage 服务器扩展的 Windows Server Web 服务器，必须先安装 FrontPage 服务器扩展。 可以通过使用 Windows Server 中管理您的服务器管理工具来执行安装。  
  
## <a name="windows-server-locked-down-content-types"></a>Windows Server：锁定的内容类型  
 上的 IIS[!INCLUDE[WinXPSvr](../includes/winxpsvr-md.md)]锁定除某些已知的内容类型 （例如，.htm、.html、.txt 等） 以外的所有文件类型。 若要启用的部署[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]使用此服务器应用程序，您需要更改 IIS 设置，以允许下载文件的类型.application、.manifest 和任何其他应用程序所使用的自定义文件类型。  
  
 如果部署使用 IIS 服务器，运行 inetmgr.exe 并添加新的默认 Web 页的文件类型：  
  
- 有关.application 和.manifest 扩展中，MIME 类型应为"应用程序/x 的 ms-应用程序。" 对于其他文件类型，MIME 类型应为"应用程序/八进制流。"  
  
- 如果使用扩展创建 MIME 类型"*"和"应用程序/八进制流"的 MIME 类型，它将允许阻止的文件类型，要下载的文件。 （但是，阻止不能下载类型，例如.aspx 和.asmx 文件）。  
  
  Windows Server 上配置 MIME 类型的具体说明，请参阅 Microsoft 知识库文章 KB326965，"IIS 6.0 不提供未知 MIME 类型"网址[ http://support.microsoft.com/default.aspx?scid=kb; en-我们; 326965](http://support.microsoft.com/default.aspx?scid=kb;en-us;326965)。  
  
## <a name="content-type-mappings"></a>内容类型映射  
 .Application 文件的内容类型 （也称为 MIME 类型） 在通过 HTTP 发布时，应为"应用程序/x 的 ms-应用程序。" 如果您有[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]安装在服务器上，这会为你自动设置。 如果未安装，则您需要创建 MIME 类型关联的[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序虚拟根 （或整个服务器）。  
  
 如果部署使用 IIS 服务器，运行 inetmgr.exe 并添加新的"应用程序/x 的 ms-应用程序"为.application 扩展名的内容类型。  
  
## <a name="http-compression-issues"></a>HTTP 压缩问题  
 使用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]，可以执行使用 HTTP 压缩的下载、 使用 GZIP 算法压缩数据流前将流发送到客户端的 Web 服务器技术。 客户端 — 在这种情况下， [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]，然后才能读取这些文件解压缩流。  
  
 如果使用 IIS，您可以轻松地启用 HTTP 压缩。 但是，当你启用 HTTP 压缩，仅启用某些文件类型，也就是说，HTML 和文本的文件。 若要启用程序集 (.dll) 的压缩，XML (.xml)、 部署清单 (.application) 和应用程序清单 (.manifest)，您必须向这些文件类型的 IIS 压缩类型的列表。 将文件类型添加到你的部署之前, 仅文本和 HTML 文件将被压缩。  
  
 有关 IIS 的详细说明，请参阅[如何指定 HTTP 压缩的其他文档类型](http://go.microsoft.com/fwlink/?LinkId=178459)。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)   
 [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
