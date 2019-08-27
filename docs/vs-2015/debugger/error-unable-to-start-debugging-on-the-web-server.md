---
title: 错误：无法在 Web 服务器上启动调试 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185474"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>错误：无法在 Web 服务器上启动调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你尝试调试的 Web 服务器上运行的 ASP.NET 应用程序时，可能会收到此错误消息：无法在 Web 服务器上启动调试。
  
在许多情况下，此错误是因为 IIS 配置不正确。

## <a name="vxtbshttpservererrorsthingstocheck"></a> 检查您的 IIS 配置

采取了解决问题，并再重新尝试调试的详细步骤之后, 您可能还需要重置 IIS。 您可以通过打开管理员命令提示符并键入实现`iisreset`，也可以执行此操作在 IIS 管理器。 

* 停止并重新启动应用程序池，然后重试。

    应用程序池可能已停止或另一个所做的配置更改可能需要你停止并重新启动应用程序池。
    
    > [!NOTE]
    > 如果应用程序池将停止，可能需要从控制面板卸载 URL 重写模块，然后重新安装它使用 Web 平台安装程序 (WPI)。 这可能是大量的系统升级后的问题。

* 请检查您的应用程序池配置，如果需要就进行更正，然后重试。

    如果密码凭据已更改，可能需要更新应用程序池中。 此外，如果最近安装了 ASP.NET，应用程序池可能会配置针对 ASP.NET 的版本错误。 解决此问题并重新启动应用程序池。
    
* 检查你的 Web 应用程序的文件夹有正确的权限。

    请确保为 IIS_IUSRS 或 IUSR （或与应用程序池相关联的特定用户） 读取和执行的 Web 应用程序文件夹的权限。 修复该问题并重新启动应用程序池。

* 如果使用本地地址使用主机文件，请尝试使用环回地址而不计算机的 IP 地址。

* 打开 localhost 页在浏览器中。

     如果未正确安装 IIS，则当你在浏览器中键入 `http://localhost` 时会收到错误。
     
     有关部署到 IIS 的信息，请参阅[Remote Debugging ASP.NET on a Remote IIS Computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)或适用于 ASP.NET Core[发布到 IIS](https://docs.asp.net/en/latest/publishing/iis.html))。

* 请确保在 IIS 上安装正确版本的 ASP.NET。  请参阅[部署 ASP.NET 应用程序](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md#BKMK_deploy_asp_net)或适用于 ASP.NET Core[发布到 IIS](https://docs.asp.net/en/latest/publishing/iis.html))。

* 在服务器上创建一个基本的 ASP.NET 应用程序。

     如果无法获取你的应用程序能够使用调试器，请尝试在服务器上本地创建基本的 ASP.NET 应用程序，尝试调试基本应用。 如果可以调试一个基本应用，可帮助您确定两个配置之间的差异。
  
* 如果只使用 IP 地址，则解决身份验证错误

     默认情况下，IP 地址被假定为 Internet 的一部分，而在 Internet 上不进行 NTLM 身份验证。 如果您的网站配置为要求身份验证的 IIS 中，此身份验证将失败。 若要更正此问题，可以指定而不是 IP 地址的远程计算机的名称。
     
## <a name="other-causes"></a>其他原因

如果使用较旧版本的 Visual Studio:

- 使用提升的权限重新启动 Visual Studio，然后重试。

    （稍后修复） 的较旧版本中的 bug 所需的一些 ASP.NET 调试方案中的提升的特权。
    
- 如果运行的 Visual Studio 的多个实例，重新打开你的 Visual Studio 中，一个实例中的项目，然后重试。

## <a name="see-also"></a>请参阅  
 [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
