---
title: 网络或代理错误的疑难解答
description: 为在防火墙或代理服务器后安装或使用 Visual Studio 时可能会遇到的网络或代理相关错误查找解决方案。
ms.date: 05/22/2019
ms.topic: troubleshooting
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs, Visual Studio
- proxy errors, Visual Studio
ms.assetid: ''
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 7879efca149c31fbe3114b0ddfcba2f2a347f5e6
ms.sourcegitcommit: 2db01751deeee7b2bdb1db25419ea6706e6fcdf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71062791"
---
# <a name="troubleshoot-network-related-errors-when-you-install-or-use-visual-studio"></a>安装或使用 Visual Studio 时与网络相关错误的疑难解答

对于你在防火墙或代理服务器后面安装或使用 Visual Studio 时，可能会遇到的最典型的与网络或代理相关的错误，我们已经有了解决方案。

## <a name="error-proxy-authorization-required"></a>错误：“所需的代理身份验证”

当用户通过代理服务器连接到 Internet，而代理服务器阻止 Visual Studio 对某些网络资源进行的调用时，通常会发生此错误。

### <a name="to-fix-this-proxy-error"></a>修复此代理错误

- 重新启动 Visual Studio。 这时会出现一个代理身份验证对话框。 出现提示时，在对话框中输入你的凭据。

- 如果重启 Visual Studio 未能解决问题，这可能是由于你的代理服务器不提示需要提供 http:&#47;&#47;go.microsoft.com 地址的凭据，而是提示需要 &#42;.visualStudio.microsoft.com 地址的凭据。 对于这些服务器，请考虑将以下 URL 添加到允许列表，以取消对 Visual Studio 中所有登录场景的阻止：

  - &#42;.windows.net

  - &#42;.microsoftonline.com

  - &#42;.visualstudio.microsoft.com

  - &#42;.microsoft.com

  - &#42;.live.com

- 否则，可以从允许列表中删除 http:&#47;&#47;go.microsoft.com 地址，以便在重启 Visual Studio 时出现代理身份验证对话框，以提供 http:&#47;&#47;go.microsoft.com 地址和服务器终结点。

  \- 或 -

- 如果你想通过代理使用默认凭据，则可以执行以下操作：

::: moniker range="vs-2017"

  1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为：%ProgramFiles%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE 或 %ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE    。

  2. 在配置文件中查找 `<system.net>` 块，然后添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      你必须在 `proxyaddress="<http://<yourproxy:port#>` 中为你的网络插入正确的代理地址。

     > [!NOTE]
     > 有关详细信息，请参阅[&lt;defaultProxy&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/)和 [proxy&lt;&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings)页。

::: moniker-end

::: moniker range="vs-2019"

  1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为：%ProgramFiles%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE 或 %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE    。

  2. 在配置文件中查找 `<system.net>` 块，然后添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      你必须在 `proxyaddress="<http://<yourproxy:port#>` 中为你的网络插入正确的代理地址。

     > [!NOTE]
     > 有关详细信息，请参阅[&lt;defaultProxy&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/)和 [proxy&lt;&gt; 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings)页。

::: moniker-end

## <a name="error-the-underlying-connection-was-closed"></a>错误：“基础连接已关闭”

如果在有防火墙的专用网络中使用 Visual Studio，则 Visual Studio 可能无法连接到某些网络资源。 这些资源可能会包括用于登录和授权的 Azure DevOps Services、NuGet 和 Azure 服务。 如果 Visual Studio 无法连接到上述某个资源，则可能出现以下错误消息：

  **基础连接已关闭：发送时出现了意外错误**

Visual Studio 使用传输层安全性 (TLS) 1.2 协议连接到网络资源。 Visual Studio 使用 TLS 1.2 时，某些专用网络上的安全设备会阻止某些服务器连接。

### <a name="to-fix-this-connection-error"></a>修复此连接错误

对以下 URL 启用连接：

- https:&#47;&#47;management.core.windows.net

- https:&#47;&#47;app.vssps.visualstudio.com

- https:&#47;&#47;login.microsoftonline.com

- https:&#47;&#47;login.live.com

- https:&#47;&#47;go.microsoft.com

- https:&#47;&#47;graph.windows.net

- https:&#47;&#47;app.vsspsext.visualstudio.com

- &#42;.azurewebsites.net（用于 Azure 连接）

- &#42;.visualstudio.microsoft.com

- cdn.vsassets.io（主机内容分发网络或 CDN、内容）

- &#42;.gallerycdn.vsassets.io（托管 Azure DevOps Services 扩展）

- static2.sharepointonline.com（Visual Studio 在字体等 Office UI Fabric 工具包中使用的主机资源）

- &#42;.nuget.org（用于 NuGet 连接）

  > [!NOTE]
  > 此列表可能未包含私人拥有的 NuGet 服务器 URL。 你可以检查在 %APPData%\Nuget\NuGet.Config 中使用的 NuGet 服务器。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [在防火墙或代理服务器后面安装和使用 Visual Studio](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [安装 Visual Studio](install-visual-studio.md)
