---
title: 错误：Web 服务器未正确配置 |Microsoft Docs
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
ms.openlocfilehash: fc0c61b766b6f93fd1321b15861000d7c628f124
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62850411"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>错误：Web 服务器配置不正确

采取此处详细说明的步骤解决问题后，在再次尝试调试之前，可能还需重置 IIS。 可通过打开管理员命令提示符并键入 `iisreset` 来执行此操作。

执行以下步骤来解决此问题：

1. 如果服务器上托管的 Web 应用程序配置为发布版本，则将其重新发布为调试版本，并验证 web.config 文件在编译元素中是否包含 `debug=true`。 重置 IIS，然后重试。

    例如，如果您将发布配置文件用于发布版本，将其更改为调试并重新发布。 否则，将调试属性设置为`false`发布时。

2. (IIS)验证物理路径正确。 在 IIS 中，找到此设置在**基本设置 > 物理路径**(或**高级设置**在较旧版本的 IIS)。

    如果复制到另一台计算机，手动重命名或移动 web 应用程序，可能不正确的物理路径。 重置 IIS，然后重试。

3. 如果您正在本地调试 Visual Studio 中，验证在属性中选择正确的服务器。 （根据项目类型，打开“属性”>“Web”>“服务器”或“属性”>“调试”。 对于 Web 窗体项目，打开“属性页”>“开始选项”>“服务器”)。

    如果使用 IIS 等外部 （自定义） 服务器，该 URL 必须是正确的。 否则，请选择 IIS Express，然后重试。

4. (IIS)请确保在服务器上安装了正确版本的 ASP.NET。

    IIS 中的ASP.NET 与 Visual Studio 项目的版本不匹配可能会导致此问题。 您可能需要在 web.config 中设置的 framework 版本。若要在 IIS 上安装 ASP.NET，请使用[Web 平台安装程序 (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx)。 另请参阅[IIS 8.0 使用 ASP.NET 3.5 和 ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)或为 ASP.NET Core [使用 IIS 的 Windows 上的主机](https://docs.asp.net/en/latest/publishing/iis.html)。

4. 如果`maxConnection`在 IIS 中的上限为过低，并有过多连接，则可能需要[增加连接限制](/iis/configuration/system.applicationhost/sites/sitedefaults/limits)。

## <a name="see-also"></a>请参阅
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)