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

通常，当用户通过代理服务器连接到 Visual Studio online 资源，而代理服务器阻止调用时，通常会发生**代理授权**错误。

若要更正此错误，请尝试执行以下一个或多个步骤：

- 重新启动 Visual Studio。 这时会出现一个代理身份验证对话框。 在对话框中输入你的凭据。

- 如果上述步骤未能解决问题，这可能是由于你的代理服务器不提示需要提供 https://go.microsoft.com 地址的凭据，而是提示需要 *.visualStudio.com 地址的凭据。 对于这些服务器，需要将以下 Url 添加到允许列表以取消阻止 Visual Studio 中的所有登录方案：

  - *.windows.net

  - *.microsoftonline.com

  - *.visualStudio.com

  - *.microsoft.com

  - *.live.com

- 可以从允许列表中删除 https://go.microsoft.com 地址，以便在重新启动 Visual Studio 时同时显示 https://go.microsoft.com 地址和服务器终结点的代理身份验证对话框。

- 如果要在代理中使用默认凭据，请执行以下操作：

   1. 查找 devenv.exe.config（devenv.exe 配置文件），查找位置为： **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE** （或 **%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Common7\IDE**）。

   2. 在配置文件中查找 `<system.net>` 块，并添加这个代码：

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress=" HYPERLINK "http://<yourproxy:port#" http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      在 `proxyaddress="<http://<yourproxy:port#>`中为你的网络插入正确的代理地址。

- 按照[此博客文章](https://blogs.msdn.microsoft.com/rido/2010/05/06/how-to-connect-to-tfs-through-authenticated-web-proxy/)中的说明添加允许你使用代理的代码。
