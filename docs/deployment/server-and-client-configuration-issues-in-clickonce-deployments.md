---
title: ClickOnce 部署中的服务器/客户端配置问题
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4ec07e71e57c0b3875d690773b7ff2618269b8f4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "88250008"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 部署中的服务器和客户端配置问题
如果你在 Windows Server 上使用 Internet Information Services (IIS) ，并且你的部署包含 Windows 无法识别的文件类型（如 Microsoft Word 文件），则 IIS 将拒绝传输该文件，并且你的部署将不会成功。

 此外，某些 Web 服务器和 Web 应用程序软件（如 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ）包含无法下载的文件和文件类型的列表。 例如， [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 阻止下载所有 *Web.config* 文件。 这些文件可能包含敏感信息，例如用户名和密码。

 尽管此限制对于下载核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 文件（如清单和程序集）没有问题，但此限制可能会阻止你下载作为应用程序一部分包含的数据文件 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 在中 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ，可以通过删除阻止从 IIS 配置管理器下载此类文件的处理程序来解决此错误。 请参阅 IIS 服务器文档了解更多详细信息。

 某些 Web 服务器可能会阻止扩展名为 *.dll*、 *.config*和 *.mdf*的文件。 基于 Windows 的应用程序通常包含具有其中一些扩展的文件。 如果用户尝试运行的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序访问 Web 服务器上的被阻止文件，将产生错误。 默认情况下，不是取消阻止所有文件扩展名 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] *。* 因此，管理员只需将 Web 服务器配置为取消阻止以下三个文件扩展名：

- *。应用程序*

- *.manifest*

- *.deploy*

  但是，你可以通过清除 "[发布选项" 对话框](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100))中的 **"使用 ' .deploy ' 文件扩展名**" 选项来禁用此选项，在这种情况下，你必须将 Web 服务器配置为取消阻止应用程序中使用的所有文件扩展名。

  例如，如果使用的是未安装 .NET Framework 的 IIS，或者使用的是其他 Web 服务器 (例如 Apache) ，则必须配置 *.manifest*、 *. application*和 *.deploy。*

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce 和安全套接字层 (SSL) 
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序将在 ssl 上正常运行，但 Internet Explorer 会引发有关 ssl 证书的提示。 当证书出现问题时，可能会引发提示，例如，当站点名称不匹配或证书已过期时。 若要 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 通过 SSL 连接进行操作，请确保证书是最新的，并且证书数据与站点数据匹配。

## <a name="clickonce-and-proxy-authentication"></a>ClickOnce 和代理身份验证
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从 .NET Framework 3.5 开始，为 Windows 集成的代理身份验证提供支持。 不需要特定的 machine.config 指令。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不提供对其他身份验证协议（如基本或摘要）的支持。

 你还可以将修补程序应用到 .NET Framework 2.0 来启用此功能。 有关详细信息，请参阅 [修复：尝试将在 .NET Framework 2.0 中创建的 ClickOnce 应用程序安装到配置为使用代理服务器的客户端计算机时，请参阅修复：错误消息： "需要代理身份验证"](https://support.microsoft.com/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that)。

 有关详细信息，请参阅[ \<defaultProxy> 网元 (网络设置) ](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)。

## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce 和 Web 浏览器兼容性
 目前， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 只有在使用 Internet Explorer 打开部署清单的 URL 时，安装才会启动。 只有在将 Internet Explorer 设置为默认 Web 浏览器的情况下，从其他应用程序（例如 Microsoft Office Outlook）启动其 URL 的部署才会成功启动。

> [!NOTE]
> 如果部署提供程序不为空或者已安装 Microsoft .NET Framework 助手扩展，则支持 Mozilla Firefox。 此扩展与 .NET Framework 3.5 SP1 一起打包。 对于 XBAP 支持，NPWPF 插件将在需要时激活。

## <a name="activate-clickonce-applications-through-browser-scripting"></a>通过浏览器脚本激活 ClickOnce 应用程序
 如果您开发了一个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用活动脚本启动应用程序的自定义网页，则您可能会发现该应用程序将不会在某些计算机上启动。 Internet Explorer 包含一个称为 " **自动提示文件下载**" 的设置，这会影响此行为。 此设置在其 "**选项**" 菜单中的 "**安全**" 选项卡上可影响此行为。 它被称为 **自动提示进行文件下载**，并在 " **下载** " 类别下面列出。 默认情况下，此属性设置为 "为 intranet Web pages **启用** "，默认情况下为 "默认 **禁用** "。 如果此设置设置为 " **禁用**"，则 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 以编程方式激活应用程序的任何尝试 (例如，通过将其 URL 分配给 `document.location` 属性) 将被阻止。 在这种情况下，用户只能通过用户启动的下载来启动应用程序，例如，通过单击超链接设置为应用程序的 URL。

## <a name="additional-server-configuration-issues"></a>其他服务器配置问题

##### <a name="administrator-permissions-required"></a>需要管理员权限
 如果要使用 HTTP 进行发布，则必须在目标服务器上具有管理员权限。 IIS 需要此权限级别。 如果不是使用 HTTP 发布，则只需要对目标路径具有写入权限。

##### <a name="server-authentication-issues"></a>服务器身份验证问题
 当您发布到禁用了 "匿名访问" 的远程服务器时，您将收到以下警告：

```
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."
```

> [!NOTE]
> 如果站点提示输入默认凭据以外的凭据，则可以使 NTLM (NT 质询-响应) 身份验证工作，并且在系统提示是否要保存提供的凭据以供将来的会话时，请单击 **"确定"** 。 但是，此解决方法不适用于基本身份验证。

## <a name="use-third-party-web-servers"></a>使用第三方 Web 服务器
 如果要 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从 IIS 之外的 Web 服务器部署应用程序，则如果服务器返回密钥文件的不正确内容类型（ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 如部署清单和应用程序清单），则可能会遇到问题。 若要解决此问题，请参阅 Web 服务器的帮助文档，了解如何向服务器添加新内容类型，并确保下表中列出的所有文件扩展名映射都已准备就绪。

|文件扩展名|内容类型|
|-------------------------|------------------|
|`.application`|`application/x-ms-application`|
|`.manifest`|`application/x-ms-manifest`|
|`.deploy`|`application/octet-stream`|
|`.msu`|`application/octet-stream`|
|`.msp`|`application/octet-stream`|

## <a name="clickonce-and-mapped-drives"></a>ClickOnce 和映射驱动器
 如果使用 Visual Studio 发布 ClickOnce 应用程序，则不能将映射驱动器指定为安装位置。 不过，你可以通过使用清单生成器和编辑器 ( # A0 和 MageUI.exe) 修改 ClickOnce 应用程序以从映射的驱动器进行安装。 有关详细信息，请参阅[Mage.exe （清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)并[MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)。

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>用于安装应用程序的 FTP 协议不受支持
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 支持从任何 HTTP 1.1 Web 服务器或文件服务器安装应用程序。 安装应用程序不支持 FTP、文件传输协议。 仅可使用 FTP 发布应用程序。 下表总结了这些差异：

| URL 类型 | 说明 |
|----------| - |
| ftp:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议发布应用程序。 |
| http:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议安装应用程序。 |
| https:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议安装应用程序。 |
| file:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议安装应用程序。 |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2： Windows 防火墙
 默认情况下，Windows XP SP2 启用 Windows 防火墙。 如果要在安装了 Windows XP 的计算机上开发应用程序，仍可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从运行 IIS 的本地服务器发布和运行应用程序。 但是，除非打开 Windows 防火墙，否则不能从另一台计算机访问运行 IIS 的服务器。 有关管理 Windows 防火墙的说明，请参阅 Windows 帮助。

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server：启用 FrontPage 服务器扩展
 若要将应用程序发布到使用 HTTP 的 Windows Web 服务器，则需要 Microsoft 提供的 FrontPage 服务器扩展。

 默认情况下，Windows Server 未安装 FrontPage 服务器扩展。 如果要使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 发布到使用 HTTP 与 FrontPage 服务器扩展的 Windows Server Web 服务器，则必须先安装 FrontPage 服务器扩展。 您可以使用 Windows Server 中的 "管理您的服务器管理工具" 执行安装。

## <a name="windows-server-locked-down-content-types"></a>Windows Server：锁定的内容类型
 IIS on [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] 锁定除某些已知内容类型之外的所有文件类型 (例如， *.htm*、 *.html*、 *.txt*等) 。 若要 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此服务器启用应用程序的部署，需要更改 IIS 设置，以允许下载类型为 *. application*、 *.manifest*和应用程序使用的任何其他自定义文件类型的文件。

 如果使用 IIS 服务器进行部署，请运行 *inetmgr.exe* 并为默认网页添加新的文件类型：

- 对于 *应用程序* 和 *清单* 扩展，MIME 类型应为 "应用程序/x 应用程序"。 对于其他文件类型，MIME 类型应为 "application/八进制流"。

- 如果创建扩展名为 " \<em> " 且 mime 类型为 "application/八进制流" 的 mime 类型，则将允许下载不受阻止的文件类型的文件。 但 (不能下载被阻止的文件类型，如* \* .aspx*和* \* .asmx* 。 ) 

  有关在 Windows Server 上配置 MIME 类型的具体说明，请参阅如何向网站 [或应用程序添加 mime 类型](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application)。

## <a name="content-type-mappings"></a>内容类型映射
 通过 HTTP 发布时，内容类型 (也称为 MIME 类型) *。应用程序* 文件应为 "应用程序/x 应用程序"。 如果在服务器上安装了 .NET Framework 2.0，将自动为您设置此设置。 如果未安装，则需要为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序 vroot (或整个服务器) 创建 MIME 类型关联。

 如果使用 IIS 服务器进行部署，请运行 <em>inetmgr。</em>exe，并为 *应用程序* 扩展添加新的 "应用程序/x 应用程序" 内容类型。

## <a name="http-compression-issues"></a>HTTP 压缩问题
 利用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，你可以执行使用 HTTP 压缩的下载，这是使用 GZIP 算法在将流发送到客户端之前压缩数据流的 Web 服务器技术。 在此示例中，客户端（在此示例中）将在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 读取文件之前对其进行解压缩。

 如果使用的是 IIS，则可以轻松启用 HTTP 压缩。 但是，当启用 HTTP 压缩时，仅对某些文件类型（即 HTML 和文本文件）启用它。 若要为程序 *集 () * 、xml (*xml*) 、部署 *清单 ()  (和* 应用 *程序清单启用* 压缩，则必须将这些文件类型添加到要压缩的 IIS 类型列表中。 将文件类型添加到部署之前，只会压缩文本和 HTML 文件。

 有关 IIS 的详细说明，请参阅 [如何为 HTTP 压缩指定其他文档类型](https://support.microsoft.com/help/234497)。

## <a name="see-also"></a>请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
