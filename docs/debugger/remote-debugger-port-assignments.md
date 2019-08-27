---
title: 远程调试器端口分配 |Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.topic: reference
ms.assetid: 238bb4ec-bb00-4c2b-986e-18ac278f3959
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 672d54b29e6de9302e88b1b95b4117783b8a0113
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903039"
---
# <a name="remote-debugger-port-assignments"></a>远程调试器端口分配
Visual Studio 远程调试器可作为应用程序或后台服务运行。 当它作为应用程序运行时，它将使用默认分配的端口，如下所示：
::: moniker range=">=vs-2019"
- Visual Studio 2019：4024
::: moniker-end
- Visual Studio 2017：4022

- Visual Studio 2015：4020

- Visual Studio 2013：4018

- Visual Studio 2012：4016

  换而言之，分配给远程调试器的端口数每个版本递增 2。 你可以根据需要设置其他端口号。 我们将在后面部分说明如何设置端口号。

## <a name="the-remote-debugger-port-on-32-bit-operating-systems"></a>32 位操作系统上的远程调试器端口

::: moniker range=">=vs-2019"
 TCP 4024（在 Visual Studio 2019 中）是所有方案都必需的主端口。 你可以在命令行或远程调试器窗口中对此进行配置。
::: moniker-end
::: moniker range="vs-2017"
 TCP 4022（在 Visual Studio 2017 中）是主端口，所有方案都必需。 你可以在命令行或远程调试器窗口中对此进行配置。
::: moniker-end

 在远程调试器窗口中，单击“工具/选项”，并设置 TCP/IP 端口号。

 在命令行中，通过 /port 开关启动远程调试器：msvsmon /port \<端口号>。

 可以在远程调试帮助（在远程调试器窗口中按 F1 或单击“帮助 > 用法”）中找到所有远程调试器命令行开关。

## <a name="the-remote-debugger-port-on-64-bit-operating-systems"></a>64 位操作系统上的远程调试器端口
::: moniker range=">=vs-2019"
 当启动远程调试器的 64 位版本时，它使用主端口 (4024) 默认情况下。  如果调试 32 位进程，64 位版远程调试器启动远程调试器端口 4025 上的 32 位版 （主端口数加 1）。 如果你运行 32 位远程调试器，它使用 4024，而不是 4025。
::: moniker-end
::: moniker range="vs-2017"
 当启动远程调试器的 64 位版本时，它使用主默认端口 (4022)。  如果调试 32 位进程，64 位版远程调试器启动远程调试器端口 4023 上的 32 位版 （主端口数加 1）。 如果运行 32 位远程调试器，它将使用 4022，而不使用 4023。
:::moniker-end

 此端口是可从命令行配置：**Msvsmon/wow64port\<端口号 >**。

## <a name="the-discovery-port"></a>发现端口
 UDP 3702 用于在网络上查找远程调试器的运行实例（例如，“附加到进程”  对话框中的“查找”  对话框）。 它仅用于发现运行远程调试器的计算机，因此如果你有某种其他方式来了解计算机名称或目标计算机的 IP 地址，它是可选的。 这是用于发现的标准端口，因此不能配置端口号。

 如果您不想要启用发现，您可以禁用发现从命令行启动 msvsmon:**Msvsmon /nodiscovery**。

## <a name="remote-debugger-ports-on-azure"></a>Azure 上的远程调试器端口
 Azure 上的远程调试器使用以下端口。 云服务上的端口映射到各 VM 上的端口。 所有端口都是 TCP。

|连接|云服务上的端口|VM 上的端口|
|-|-|-|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector|30400|30398|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarder|31400|31398|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarderx86|31401|31399|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.FileUpload|32400|32398|

## <a name="see-also"></a>请参阅
- [远程调试](../debugger/remote-debugging.md)