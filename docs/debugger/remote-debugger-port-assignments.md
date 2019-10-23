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
ms.openlocfilehash: cf3d3ce704d517224452731c52a891ac2263f738
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72730243"
---
# <a name="remote-debugger-port-assignments"></a>远程调试器端口分配
Visual Studio 远程调试器可作为应用程序或后台服务运行。 当它作为应用程序运行时，它将使用默认分配的端口，如下所示：
::: moniker range=">=vs-2019"
- Visual Studio 2019: 4024
::: moniker-end
- Visual Studio 2017: 4022

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
 当启动64位版本的远程调试器时，它默认使用主端口（4024）。  如果调试32位进程，则64位版本的远程调试器将在端口4025（主端口号递增1）上启动一个32位版本的远程调试器。 如果你运行 32 位远程调试器，它使用 4024，而不是 4025。
::: moniker-end
::: moniker range="vs-2017"
 当启动64位版本的远程调试器时，它默认使用主端口（4022）。  如果调试32位进程，则64位版本的远程调试器将在端口4023（主端口号递增1）上启动一个32位版本的远程调试器。 如果运行 32 位远程调试器，它将使用 4022，而不使用 4023。
:::moniker-end

 此端口可在命令行中进行配置：Msvsmon /wow64port \<端口号>。

## <a name="the-discovery-port"></a>发现端口
 UDP 3702 用于在网络上查找远程调试器的运行实例（例如，“附加到进程” 对话框中的“查找” 对话框）。 它仅用于发现运行远程调试器的计算机，因此如果你有某种其他方式来了解计算机名称或目标计算机的 IP 地址，它是可选的。 这是用于发现的标准端口，因此不能配置端口号。

 如果你不想启用发现，可以在禁用发现的情况下从命令行启动 msvsmon：  **Msvsmon /nodiscovery**。

## <a name="remote-debugger-ports-on-azure"></a>Azure 上的远程调试器端口
 Azure 上的远程调试器使用以下端口。 云服务上的端口映射到各 VM 上的端口。 所有端口都是 TCP。

|连接|云服务上的端口|VM 上的端口|
|-|-|-|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector|30400|30398|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarder|31400|31398|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.Forwarderx86|31401|31399|
|Microsoft.WindowsAzure.Plugins.RemoteDebugger.FileUpload|32400|32398|

## <a name="see-also"></a>请参阅
- [Remote Debugging](../debugger/remote-debugging.md)