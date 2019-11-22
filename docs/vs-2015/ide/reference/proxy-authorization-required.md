---
title: 所需的代理身份验证 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
ms.assetid: c2d24ae1-9902-460e-b72a-0299eed9ee82
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 848817691d7fae32f2240e3d6cac4451c4ce58c4
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297810"
---
# <a name="proxy-authorization-required"></a>所需的代理身份验证
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

The **Proxy authorization required** error generally occurs when users are connected to Visual Studio online resources through a proxy server, and the proxy server blocks the calls.

To correct this error, try one or more of the following steps:

- 重新启动 Visual Studio。 这时会出现一个代理身份验证对话框。 在对话框中输入你的凭据。

- 如果上述步骤未能解决问题，这可能是由于你的代理服务器不提示需要提供 https://go.microsoft.com 地址的凭据，而是提示需要 *.visualStudio.com 地址的凭据。 For these servers, you need to add the following URLs to the allow list to unblock all sign-in scenarios in Visual Studio:

  - *.windows.net

  - *.microsoftonline.com

  - *.visualstudio.com

  - *.microsoft.com

  - *.live.com

- You can remove the https://go.microsoft.com address from the allow list so that the proxy authentication dialog shows up for both the https://go.microsoft.com address and the server endpoints when Visual Studio is restarted.

- If you want to use your default credentials with your proxy, do the following:

   1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为： **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE** （或 **%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Common7\IDE**）。

   2. 在配置文件中查找 `<system.net>` 块，并添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress=" HYPERLINK "http://<yourproxy:port#" http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      Insert the correct proxy address for your network in `proxyaddress="<http://<yourproxy:port#>`.

- Follow the instructions in [this blog post](https://blogs.msdn.microsoft.com/rido/2010/05/06/how-to-connect-to-tfs-through-authenticated-web-proxy/) to add code that allows you to use the proxy.
