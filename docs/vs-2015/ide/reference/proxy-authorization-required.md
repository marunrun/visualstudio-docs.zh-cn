---
title: 所需的代理身份验证 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
ms.assetid: c2d24ae1-9902-460e-b72a-0299eed9ee82
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f2de40c520bca0ea04f50ec782fec2dda531172e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67822071"
---
# <a name="proxy-authorization-required"></a>所需的代理身份验证
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**所需的代理身份验证**错误通常发生在用户连接到 Visual Studio online 资源通过代理服务器，而代理服务器对调用进行阻止。

若要更正此错误，请尝试一个或多个以下步骤：

- 重新启动 Visual Studio。 这时会出现一个代理身份验证对话框。 在对话框中输入你的凭据。

- 如果上述步骤未能解决问题，这可能是由于你的代理服务器不提示需要提供 http://go.microsoft.com 地址的凭据，而是提示需要 *.visualStudio.com 地址的凭据。 对于这些服务器，需要以下 Url 添加到允许列表以取消阻止在 Visual Studio 中的所有登录方案：

  - *.windows.net

  - *.microsoftonline.com

  - *.visualstudio.com

  - *.microsoft.com

  - *.live.com

- 您可以删除 [http://go.microsoft.com](http://go.microsoft.com ) 地址的允许列表中，以便同时显示代理身份验证对话框 [http://go.microsoft.com](http://go.microsoft.com ) 地址和服务器终结点时重新启动 Visual Studio。

- 如果你想要通过代理使用默认凭据，请执行以下操作：

   1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为： **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE** （或 **%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Common7\IDE**）。

   2. 在配置文件中查找 `<system.net>` 块，并添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress=" HYPERLINK "http://<yourproxy:port#" http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      插入您的网络中的正确的代理地址`proxyaddress="<http://<yourproxy:port#>`。

- 按照中的说明[这篇博客文章](http://blogs.msdn.com/b/rido/archive/2010/05/06/how-to-connect-to-tfs-through-authenticated-web-proxy.aspx)添加代码，您可以使用代理服务器。
