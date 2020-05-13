---
title: 配置 Windows 防火墙以进行远程调试 |Microsoft Docs
ms.date: 10/31/2018
ms.topic: conceptual
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff64735e1711a18bd7c55c6e052fa8579bd12e16
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563716"
---
# <a name="configure-windows-firewall-for-remote-debugging"></a>配置 Windows 防火墙以进行远程调试

在受 Windows 防火墙保护的网络上，必须将防火墙配置为允许远程调试。 Visual Studio 和远程调试工具会尝试在安装或启动期间打开正确的防火墙端口，但可能还需要手动打开端口或允许应用。

本主题介绍如何在 Windows 10、8/8.1 和 7 以及 Windows Server 2012 R2、2012 和 2008 R2 计算机上配置 Windows 防火墙，以进行远程调试。 Visual Studio 和远程计算机无需运行相同的操作系统。 例如，运行 Visual Studio 的计算机可以使用 Windows 10 ，而远程计算机可以运行 Windows Server 2012 R2。

>[!NOTE]
>对于不同的操作系统和旧版 Windows，配置 Windows 防火墙的说明略有不同。 Windows 8/8.1、Windows 10 和 Windows Server 2012 设置使用“*应用*”一词，而 Windows 7 和 Windows Server 2008 使用“*程序*”一词。

## <a name="configure-ports-for-remote-debugging"></a>配置用于远程调试的端口

Visual Studio 和远程调试器会尝试在安装或启动期间打开正确的端口。 但在某些情况下（例如第三方防火墙），可能需要手动打开端口。

**若要打开的端口：**

1. 在 Windows“开始”菜单中，搜索并打开“高级安全 Windows 防火墙”。 在 Windows 10 中，则是“高级安全性 Windows Defender 防火墙”。

1. 对于新的传入端口，选择“入站规则”，然后选择“新建规则”。 对于传出端口，则选择“出站规则”。

1. 在“新建入站规则向导”中，选择“端口”，然后选择“下一步”。

1. 根据后面的表中的端口号，选择“TCP”或“UDP”。

1. 在“特定本地端口”下，输入后面的表中的一个端口号，然后选择“下一步”。

1. 选择“允许连接”，然后选择“下一步”。

1. 选择要启用的一种或多种网络类型，包括远程连接的网络类型，然后选择“下一步”。

1. 为规则添加一个名称（例如， **msvsmon**、**IIS** 或 **Web Deploy**），然后选择“完成”。

   新规则应出现在“入站规则”或“出站规则”列表中，且处于选中状态。

### <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>远程计算机上支持远程调试的端口

对于远程调试，必须在远程计算机上打开以下端口：

::: moniker range="vs-2017"

|**端口**|**传入/传出**|**协议**|**说明**|
|-|-|-|-|
|4022|传入|TCP|用于 VS 2017。 端口号针对每个 Visual Studio 版本递增 2。 有关详细信息，请参阅 [Visual Studio 远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。|
|4023|传入|TCP|用于 VS 2017。 端口号针对每个 Visual Studio 版本递增 2。 此端口是仅用于远程调试从 64 位版本的远程调试器的 32 位进程。 有关详细信息，请参阅 [Visual Studio 远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。|
|3702|传出|UDP|（可选）进行远程调试器发现的必需项。|

::: moniker-end

::: moniker range=">= vs-2019"

|**端口**|**传入/传出**|**协议**|**说明**|
|-|-|-|-|
|4024|传入|TCP|用于 VS 2019。 端口号针对每个 Visual Studio 版本递增 2。 有关详细信息，请参阅 [Visual Studio 远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。|
|4025|传入|TCP|用于 VS 2019。 端口号针对每个 Visual Studio 版本递增 2。 此端口是仅用于远程调试从 64 位版本的远程调试器的 32 位进程。 有关详细信息，请参阅 [Visual Studio 远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。|
|3702|传出|UDP|（可选）进行远程调试器发现的必需项。|

::: moniker-end

如果在“工具” > ”选项” > “调试”下选择“使用托管兼容模式”，请打开这些附加远程调试器端口。 调试器托管兼容模式支持旧版 Visual Studio 2010 版本的调试器。

|**端口**|**传入/传出**|**协议**|**说明**|
|-|-|-|-|
|135, 139, 445|传出|TCP|必需。|
|137, 138|传出|UDP|必需。|

如果您的域策略要求通过 IPSec 进行网络通信，则必须打开 Visual Studio 和远程计算机上的其他端口。 若要调试远程 IIS web 服务器上，打开远程计算机上的端口 80。

|**端口**|**传入/传出**|**协议**|**说明**|
|-|-|-|-|
|500, 4500|传出|UDP|如果你的域策略需要通过 IPSec 进行网络通信，则需要。|
|80|传出|TCP|Web 服务器调试所必需。|

若要允许特定应用通过 Windows 防火墙，请参阅[配置通过 Windows 防火墙的远程调试](#configure-remote-debugging-through-windows-firewall)。

## <a name="configure-remote-debugging-through-windows-firewall"></a>配置 Windows 防火墙以进行远程调试

可以在远程计算机上安装远程调试工具，或从共享文件夹运行它们。 在任一情况下，必须正确配置远程计算机防火墙。

在远程计算机上远程调试工具将位于：

*\<Visual Studio 安装目录\>\\Common7\\IDE\\远程调试器\\\<x86*， *x64*，或*Appx*\>

### <a name="allow-and-configure-the-remote-debugger-through-windows-firewall"></a>配置并允许远程调试器通过 Windows 防火墙

1. 在 Windows“开始”菜单中，搜索并打开“Windows 防火墙”或“Windows Defender 防火墙”。 

1. 选择“允许应用通过 Windows 防火墙”。

1. 如果**远程调试器**或**Visual Studio 远程调试器**未显示在**允许的应用程序和功能**，选择**更改设置**，然后选择**允许另一个应用**。

1. 如果远程调试器应用程序仍未列出在**将应用添加**对话框中，选择**浏览**，并导航到 *\<Visual Studio 安装目录\>\\Common7\\IDE\\远程调试器\\\<x86*， *x64*，或*Appx* \>具体取决于您的应用程序的适当体系结构。 选择*msvsmon.exe*，然后选择**添加**。

1. 在中**应用程序**列表中，选择**远程调试器**刚添加的。 选择**网络类型**，然后选择一个或多个网络类型，包括远程连接的网络类型。

1. 选择**外**，然后选择**确定**。

## <a name="troubleshooting"></a>远程调试连接进行故障排除

如果无法使用远程调试器附加到您的应用，请确保远程调试的防火墙端口、协议、网络类型和应用设置均正确无误。

- 在 Windows“开始”菜单中，搜索并打开“Windows 防火墙”，然后选择“允许应用通过 Windows 防火墙”。 请确保“远程调试器”或“Visual Studio 远程调试器”出现在“允许的应用和功能”列表中并且其复选框已选中，同时选择了网络类型。 如果不是这样，请[添加正确的应用和设置](#configure-remote-debugging-through-windows-firewall)。

- 在 Windows“开始”菜单中，搜索并打开“高级安全 Windows 防火墙”。 请确保“远程调试器”或“Visual Studio 远程调试器”在“入站规则”和“出站规则”（可选）下显示并带有绿色的复选标记图标，以及确保所有设置正确。

  - 若要查看或更改规则设置，请右键单击**远程调试器**应用程序在列表中，选择**属性**。 使用**属性**选项卡来启用或禁用规则，或更改端口号、 协议或网络类型。
  - 如果规则列表中看不到远程调试器应用[添加并配置了正确的端口](#configure-ports-for-remote-debugging)。

## <a name="see-also"></a>请参阅

- [远程调试](../debugger/remote-debugging.md)
- [Visual Studio 远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
