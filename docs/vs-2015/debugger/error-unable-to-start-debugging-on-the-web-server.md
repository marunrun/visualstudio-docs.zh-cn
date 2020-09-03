---
title: 错误：无法在 Web 服务器上启动调试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.http
- vwd.nonadmin.error.
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- IIS, debugging DLLs
- debugger, Web application errors
- unable to start debugging error
- security [debugger], Web applications
- debugging [Visual Studio], errors
- HTTP servers, debugging error
- security settings, checking for default Web sites
- errors [debugger], unable to start debugging
- debugging ASP.NET Web applications, unable to start debugging error
- remote debugging, errors
ms.assetid: f62e378a-3a99-4f78-9d97-8bb63a4da181
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0b0cbd7afe90b1dbc091263e3a2594c9ca739e1c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185474"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>错误：无法在 Web 服务器上启动调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你尝试调试在 Web 服务器上运行的 ASP.NET 应用程序时，可能会收到此错误消息：无法在 Web 服务器上启动调试。
  
在许多情况下，出现此错误的原因是未正确配置 IIS。

## <a name="check-your-iis-configuration"></a><a name="vxtbshttpservererrorsthingstocheck"></a> 检查 IIS 配置

采取步骤解决此处详细介绍的问题后，在再次尝试调试之前，可能还需要重置 IIS。 你可以通过打开管理员命令提示符并键入来完成 `iisreset` 此操作，也可以在 IIS 管理器中执行此操作。 

* 停止并重新启动应用程序池，然后重试。

    应用程序池可能已停止，或者你所做的另一种配置更改可能要求你停止并重新启动应用程序池。
    
    > [!NOTE]
    > 如果应用程序池继续停止，可能需要从 "控制面板" 中卸载 URL 重写模块，然后使用 Web 平台安装程序 (WPI) 重新安装它。 这可能是在进行大量系统升级后出现的问题。

* 请检查您的应用程序池配置，如果需要就进行更正，然后重试。

    如果密码凭据已更改，则可能需要在应用程序池中更新它们。 此外，如果最近安装了 ASP.NET，则可能会针对错误的 ASP.NET 版本配置应用程序池。 解决问题，然后重新启动应用程序池。
    
* 检查 Web 应用程序文件夹是否具有适当的权限。

    请确保为 IIS_IUSRS 或 IUSR (或与应用程序池关联的特定用户) "Web 应用程序" 文件夹的 "读取" 和 "执行" 权限。 修复该问题并重新启动应用程序池。

* 如果使用的是具有本地地址的 HOSTS 文件，请尝试使用环回地址，而不是计算机的 IP 地址。

* 在浏览器中打开 localhost 页。

     如果未正确安装 IIS，则当你在浏览器中键入 `http://localhost` 时会收到错误。
     
     有关部署到 IIS 的详细信息，请参阅远程 [调试 ASP.NET 在远程 IIS 计算机上](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) ，或者，对于 ASP.NET Core [发布到 iis](https://docs.asp.net/en/latest/publishing/iis.html)) 。

* 请确保在 IIS 上安装了正确版本的 ASP.NET。  [若要](https://docs.asp.net/en/latest/publishing/iis.html)ASP.NET Core，请参阅[部署 ASP.NET 应用程序](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md#BKMK_deploy_asp_net)) 。

* 在服务器上创建一个基本 ASP.NET 应用程序。

     如果无法让应用使用调试器，请尝试在服务器上本地创建基本 ASP.NET 应用程序，并尝试对其进行调试。 如果可以调试基本应用，这可能会帮助你确定两种配置的不同之处。
  
* 如果只使用 IP 地址，则解决身份验证错误

     默认情况下，IP 地址被假定为 Internet 的一部分，而在 Internet 上不进行 NTLM 身份验证。 如果你的网站已在 IIS 中配置为需要身份验证，则此身份验证将失败。 若要更正此问题，可以指定远程计算机的名称，而不是 IP 地址。
     
## <a name="other-causes"></a>其他原因

如果你使用的是较旧版本的 Visual Studio：

- 请用提升的权限重启 Visual Studio，然后重试。

    早期版本中的 bug (稍后修复) 必需的提升权限。
    
- 如果 Visual Studio 的多个实例正在运行，请在一个 Visual Studio 实例中重新打开项目，然后重试。

## <a name="see-also"></a>另请参阅  
 [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
