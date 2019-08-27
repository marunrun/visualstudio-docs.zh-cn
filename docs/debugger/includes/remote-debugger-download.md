---
title: 远程调试器下载
description: 远程调试器的下载链接
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 1e90a1d9e03892cf81bd2257d3dcc6e25ab36246
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149198"
---
在远程设备或服务器，你想要调试，而非 Visual Studio 计算机，下载并安装远程工具的正确版本从下表中的链接。

- 下载最新版本的 Visual Studio 远程工具。 最新的远程工具版本兼容使用早期的 Visual Studio 版本，但早期的远程工具版本不是与更高版本的 Visual Studio 版本兼容。 （例如，如果使用 Visual Studio 2017，下载适用于 Visual Studio 2017 远程工具的最新的更新。 在此方案中，不要下载远程工具的 Visual Studio 2019。）
- 下载的远程工具使用相同的体系结构在计算机安装它们。 例如，如果你想要调试远程计算机运行 64 位操作系统上的 32 位应用程序，安装 64 位远程工具。

::: moniker range=">=vs-2019"

|Version|链接|说明|
|-|-|-|
|Visual Studio 2019|[远程工具](https://visualstudio.microsoft.com/downloads#remote-tools-for-visual-studio-2019)|与所有 Visual Studio 2019 版本兼容。 下载匹配您设备的操作系统 (x 86、 x64、 或 ARM64） 的版本。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)下载远程工具的帮助。|
|Visual Studio 2017|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|与所有 Visual Studio 2017 版本兼容。 下载匹配您设备的操作系统 (x 86、 x64、 或 ARM64） 的版本。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)下载远程工具的帮助。|
|Visual Studio 2015|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 远程工具可从 My.VisualStudio.com。 如果系统提示，请加入免费[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)程序或使用 Visual Studio 订阅 id。 登录 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)下载远程工具的帮助。|
|Visual Studio 2013|[远程工具](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|下载 Visual Studio 2013 文档中的页|
|Visual Studio 2012|[远程工具](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|下载 Visual Studio 2012 文档中的页|

::: moniker-end

::: moniker range="vs-2017"

|Version|链接|说明|
|-|-|-|
|Visual Studio 2017|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|与所有 Visual Studio 2017 版本兼容。 下载匹配您设备的操作系统 (x 86、 x64、 或 ARM64） 的版本。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)下载远程工具的帮助。 有关远程工具的最新版本，打开[Visual Studio 2019 doc](../../debugger/remote-debugging.md?view=vs-2019)。|
|Visual Studio 2015|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 远程工具可从 My.VisualStudio.com。 如果系统提示，请加入免费[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)程序或使用 Visual Studio 订阅 id。 登录 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)下载远程工具的帮助。|
|Visual Studio 2013|[远程工具](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|下载 Visual Studio 2013 文档中的页|
|Visual Studio 2012|[远程工具](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|下载 Visual Studio 2012 文档中的页|

::: moniker-end

复制可运行远程调试器*msvsmon.exe*到远程计算机，而不是安装远程工具。 但是，远程调试器配置向导 (*rdbgwiz.exe*) 可仅当安装远程工具。 您可能需要使用该向导进行配置，如果你想要远程调试器作为服务运行。 有关详细信息，请参阅[（可选） 配置远程调试器作为服务](../../debugger/remote-debugging.md#bkmk_configureService)。

>[!NOTE]
>- 若要调试 ARM 设备上的 Windows 10 应用，使用 ARM64，这是可用的远程工具的最新版本。
>- 若要调试在 Windows RT 设备上的 Windows 10 应用，使用 ARM，仅在 Visual Studio 2015 远程工具下载中可用。
