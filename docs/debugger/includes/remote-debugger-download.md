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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149198"
---
在要调试的远程设备或服务器上（而不是 Visual Studio 计算机上），请从下表中的链接下载并安装正确的远程工具版本。

- 下载适合 Visual Studio 版本的最新远程工具。 最新的远程工具版本与早期的 Visual Studio 版本兼容，但早期的远程工具版本与后来的 Visual Studio 版本不兼容。 （例如，如果使用的是 Visual Studio 2017，请下载 Visual Studio 2017 远程工具的最新更新。 在这种情况下，请不要下载 Visual Studio 2019 的远程工具。）
- 下载与要安装远程工具的计算机具有相同体系结构的远程工具。 例如，如果要在运行 64 位操作系统的远程计算机上调试 32 位应用，请安装 64 位远程工具。

::: moniker range=">=vs-2019"

|Version|链接|说明|
|-|-|-|
|Visual Studio 2019|[远程工具](https://visualstudio.microsoft.com/downloads#remote-tools-for-visual-studio-2019)|兼容所有 Visual Studio 2019 版本。 下载与设备操作系统（x86、x64 或 ARM64）匹配的版本。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)，获取有关下载远程工具的帮助。|
|Visual Studio 2017|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|兼容所有 Visual Studio 2017 版本。 下载与设备操作系统（x86、x64 或 ARM64）匹配的版本。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)，获取有关下载远程工具的帮助。|
|Visual Studio 2015|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 的远程工具可从 My.VisualStudio.com 获取。 如果出现提示，请加入免费的 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) 计划，或使用 Visual Studio 订阅 ID 登录。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)，获取有关下载远程工具的帮助。|
|Visual Studio 2013|[远程工具](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Visual Studio 2013 文档中的下载页面|
|Visual Studio 2012|[远程工具](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Visual Studio 2012 文档中的下载页面|

::: moniker-end

::: moniker range="vs-2017"

|Version|链接|说明|
|-|-|-|
|Visual Studio 2017|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|兼容所有 Visual Studio 2017 版本。 下载与设备操作系统（x86、x64 或 ARM64）匹配的版本。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)，获取有关下载远程工具的帮助。 有关最新版本远程工具的信息，请打开 [Visual Studio 2019 文档](../../debugger/remote-debugging.md?view=vs-2019)。|
|Visual Studio 2015|[远程工具](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 的远程工具可从 My.VisualStudio.com 获取。 如果出现提示，请加入免费的 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) 计划，或使用 Visual Studio 订阅 ID 登录。 在 Windows 服务器上，请参阅[取消阻止文件下载](../../debugger/remote-debugging-unblock-file-download.md)，获取有关下载远程工具的帮助。|
|Visual Studio 2013|[远程工具](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Visual Studio 2013 文档中的下载页面|
|Visual Studio 2012|[远程工具](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Visual Studio 2012 文档中的下载页面|

::: moniker-end

可以通过将 msvsmon.exe 复制到远程计算机，而不是安装远程工具来运行远程调试器。 但是，远程调试器配置向导 (rdbgwiz.exe) 仅在安装远程工具时才可用。 如果要将远程调试器作为服务运行，则可能需要使用向导进行配置。 有关详细信息，请参阅[（可选）将远程调试器配置为服务](../../debugger/remote-debugging.md#bkmk_configureService)。

>[!NOTE]
>- 若要在 ARM 设备上调试 Windows 10 应用，请使用 ARM64，它可用于最新版本的远程工具。
>- 若要在 Windows RT 设备上调试 Windows 10 应用，请使用 ARM，它仅在 Visual Studio 2015 远程工具下载中可用。
