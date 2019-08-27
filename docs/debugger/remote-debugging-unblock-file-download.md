---
title: 取消阻止远程工具下载
ms.date: 07/19/2018
ms.topic: troubleshooting
helpviewer_keywords:
- remote debugging, unblock download
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a243033bf5831952d83fdf688302651e02b76b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903014"
---
# <a name="how-to-unblock-the-download-of-the-remote-tools-on-windows-server"></a>如何：取消阻止 Windows Server 上的远程工具下载

在 Windows Server 上的 Internet Explorer 中的默认安全设置可以使下载组件，如远程工具实现起来非常耗时。

* 在 Internet Explorer，可防止打开网站和访问 web 资源，除非显式允许包含资源的域上启用增强的安全配置 （即，受信任）。 尽管你可以禁用此设置，但我们不建议这样做因为它可能会造成安全风险。

* 在 Windows Server 2016 中，默认值中设置**Internet 选项** > **安全** > **Internet**  >  **自定义级别** > **下载**还禁用文件下载。 如果你选择下载直接在 Windows Server 上的远程工具，则必须启用文件下载。

若要下载 Windows Server 上的工具，我们建议以下之一：

* 下载一个正在运行 Visual Studio 中，如在其他计算机上的远程工具，然后将复制 *.exe*到 Windows Server 的文件。

* 运行远程调试器[从文件共享](../debugger/remote-debugging.md#fileshare_msvsmon)在 Visual Studio 计算机上。

* 下载直接在 Windows Server 上的远程工具，然后按提示以添加受信任的站点。 新式网站通常包括许多第三方资源，因此这可能会导致大量提示。 此外，可能需要手动添加任何重定向的链接。 您可以选择在开始下载之前添加一些受信任的站点。 转到**Internet 选项 > 安全性 > 受信任的站点 > 站点**并添加以下站点。

  * visualstudio.microsoft.com
  * download.visualstudio.microsoft.com
  * 有关： 空白

  对于较旧版本的上 my.visualstudio.com 调试器中，添加这些其他站点，以确保该登录名是成功：

  * microsoft.com
  * go.microsoft.com
  * download.microsoft.com
  * my.visualstudio.com
  * login.microsoftonline.com
  * login.live.com
  * secure.aadcdn.microsoftonline-p.com
  * msft.sts.microsoft.com
  * auth.gfx.ms
  * app.vssps.visualstudio.com
  * vlscppe.microsoft.com
  * query.prod.cms.rt.microsoft.com

    如果你选择下载的远程工具时添加这些域，然后选择**添加**出现提示时。

    ![阻止内容对话框](../debugger/media/remotedbg-blocked-content.png)

    下载软件时，可以获取一些额外的请求授予权限以加载各种 web 站点脚本和资源。 上 my.visualstudio.com，我们建议您添加其他的域，以确保该登录名是成功。