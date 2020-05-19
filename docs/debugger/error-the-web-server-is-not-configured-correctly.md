---
title: 错误：Web 服务器配置不正确 | Microsoft Docs
ms.date: 09/20/2017
ms.topic: troubleshooting
f1_keywords:
- vs.debug.remote.projnotconfigured
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be5db0a08a287e2611c29396e96e72719b5106a7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736928"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>错误：Web 服务器配置不正确

采取此处详细说明的步骤解决问题后，在再次尝试调试之前，可能还需重置 IIS。 可通过打开管理员命令提示符并键入 `iisreset` 来执行此操作。

请采取以下步骤来解决此问题：

1. 如果服务器上托管的 Web 应用程序配置为发布版本，则将其重新发布为调试版本，并验证 web.config 文件在编译元素中是否包含 `debug=true`。 重置 IIS，然后重试。

    例如，如果使用发布版本的发布配置文件，请将其更改为调试，并重新发布。 否则，在发布时，调试属性将设置为 `false`。

2. (IIS) 验证物理路径是否正确。 在 IIS 中，可在“基本设置”>“物理路径”（或较早版本 IIS 中的“高级设置”）中找到此设置 。

    如果将 Web 应用程序复制到另一台计算机、手动重命名或移动，则物理路径可能不正确。 重置 IIS，然后重试。

3. 如果要在 Visual Studio 中进行本地调试，请验证是否在属性中选择了正确的服务器。 （根据项目类型，打开“属性”>“Web”>“服务器”或“属性”>“调试”。 对于 Web 窗体项目，打开“属性页”>“开始选项”>“服务器”)。

    如果使用的是外部（自定义）服务器（如 IIS），URL 必须正确。 否则，请选择 IIS Express，然后重试。

4. (IIS) 请确保在服务器上安装了正确的 ASP.NET 版本。

    IIS 中的ASP.NET 与 Visual Studio 项目的版本不匹配可能会导致此问题。 可能需要在 web.config 中设置框架版本。若要在 IIS 上安装 ASP.NET，请使用 [Web 平台安装程序 (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx)。 另请参阅[IIS 8.0 使用 ASP.NET 3.5 和 ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)或为 ASP.NET Core [使用 IIS 的 Windows 上的主机](https://docs.asp.net/en/latest/publishing/iis.html)。

4. 如果 IIS 中的 `maxConnection` 限制过低且你的连接过多，则可能需要[增加连接限制](/iis/configuration/system.applicationhost/sites/sitedefaults/limits)。

## <a name="see-also"></a>请参阅
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)