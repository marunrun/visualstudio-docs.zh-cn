---
title: 配置 Windows 防火墙以允许远程调试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8f41aa8c074f724976adabaa99df0e8ca0064fa3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161543"
---
# <a name="configure-the-windows-firewall-for-remote-debugging"></a>配置 Windows 防火墙以便进行远程调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍如何配置防火墙以在运行以下操作系统的计算机上启用远程调试：  
  
- Windows 7  
  
- Windows 8/8.1  
  
- Windows 10  
  
- Windows Server 2008 (R2)  
  
- Windows Server 2012  
  
- Windows Server 2012 R2  
  
  如果正在调试的网络不受防火墙保护，则此配置是不必要的。 否则，承载 Visual Studio 的计算机和要调试的远程计算机均需要对防火墙配置的更改。  
  
  “”  If your network requires that communication be performed using , you must open additional ports on both the Visual Studio host computer and the remote computer.  
  
  “Web 服务器”  如果你正在调试远程 Web 服务器，则必须打开远程计算机上的其他端口。  
  
  请注意，这两台计算机不需要运行相同的操作系统。 例如，Visual Studio 计算机可以运行 Windows 10，而远程计算机可以运行 Windows Server 2012 R2。  
  
## <a name="to-configure-windows-firewall-on-the-visual-studio-computer"></a>若要在 Visual Studio 计算机上配置 Windows 防火墙  
 有关配置 Windows 防火墙的说明在不同操作系统上略有不同。 在 Windows 7 或 Windows Server 2008 中，使用 **程序** 一词；而在 Windows 8/8.1、Windows 10 和 Windows Server 2012 中，使用 **应用** 一词。  在以下步骤中，我们将使用 **应用**一词。  
  
1. 打开 Windows 防火墙页。 （在“启动”  菜单搜索框中，键入“Windows 防火墙”  。）  
  
2. 单击“允许应用或功能通过 Windows 防火墙”  。  
  
3. 在“允许的应用和功能”  列表中，查找“Visual Studio 远程调试器发现”  。 如果已列出，请确保该选项被选中，并且同时选中一个或多个网络类型。  
  
4. 如果未列出“Visual Studio 远程调试器发现”  ，请单击“允许其他应用”  。 如果你仍未看到它在**将应用添加**窗口中，单击**浏览**，并导航到 **\<Visual Studio 安装目录 > \Common7\IDE\Remote 调试器**. 为应用程序 (x86, x64, Appx) 查找适当的文件夹，然后选择“msvsmon.exe”  。 然后单击 **“添加”** 。  
  
5. 在“允许的应用和功能”  列表中，选择“Visual Studio 远程调试监视器”  。 检查你希望远程调试监视器与之进行通信的一个或多个网络类型（“域”、“家庭/工作”（专用）、“公用”  ）。 类型必须包括 Visual Studio 计算机连接到的网络。  
  
## <a name="to-open-a-port-on-the-visual-studio-computer-to-enable-discovery"></a>若要打开 Visual Studio 计算机上的端口以启用发现  
 你必须允许 UDP 端口 3702 传入，以允许运行远程调试器的计算机的发现。 若要将其添加，请参阅如何在防火墙中配置端口。  
  
## <a name="to-configure-the-windows-firewall-of-the-remote-computer-for-remote-debugging"></a>若要配置远程计算机的 Windows 防火墙以进行远程调试  
 远程调试组件可在远程计算机上安装或从共享目录中运行。 在这两种情况下都必须配置远程计算机的防火墙。 远程调试组件位于：  
  
 **\<Visual Studio 安装目录 > \Common7\IDE\Remote 调试器**  
  
 有关配置 Windows 防火墙的说明在不同操作系统上略有不同。 在 Windows 7 或 Windows Server 2008 中，使用 **程序** 一词；而在 Windows 8/8.1、Windows 10 和 Windows Server 2012 中，使用 **应用** 一词。  在以下步骤中，我们将使用 **应用**一词。  
  
1. 打开 Windows 防火墙页。 （在“启动”  菜单搜索框中，键入“Windows 防火墙”  。）  
  
2. 单击“允许应用或功能通过 Windows 防火墙”  。  
  
3. 在“允许的应用和功能”  列表中，查找“Visual Studio 远程调试监视器”  。 如果已列出，请确保该选项被选中，并且同时选中一个或多个网络类型。  
  
4. 如果未列出“Visual Studio 远程调试监视器”  ，请单击“允许另一个应用”  。 如果你仍未看到它在**添加应用程序窗口**，单击**浏览**，并导航到 **\<Visual Studio 安装目录 > \Common7\IDE\Remote 调试器**. 为应用程序 (x86, x64, Appx) 查找适当的文件夹，然后选择“msvsmon.exe”  。 然后单击 **“添加”** 。  
  
5. 在“允许的应用”  列表中，选择“Visual Studio 远程调试监视器”  。 检查你希望远程调试监视器与之进行通信的一个或多个网络类型（“域”、“家庭/工作”（专用）、“公用”  ）。 类型必须包括 Visual Studio 计算机连接到的网络。  
  
## <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>远程计算机上支持远程调试的端口  
  
|||||  
|-|-|-|-|  
|**端口**|**传入/传出**|**协议**|**说明**|  
|3702|传出|UDP|远程调试器发现所必需的。|  
|4020||TCP|用于 VS 2015。 端口号针对每个 Visual Studio 版本递增 2。 有关详细信息，请参阅“Visual Studio 远程调试器端口分配”。|  
|4021||TCP|用于 VS 2015。 端口号针对每个 Visual Studio 版本递增 2。 有关详细信息，请参阅“Visual Studio 远程调试器端口分配”。|  
  
## <a name="ports-on-the-remote-computer-that-enable-remote-debugging-with-managed-or-native-compatibility-mode"></a>远程计算机上的端口，这些端口启用托管或本机兼容性模式的远程调试  
  
|||||  
|-|-|-|-|  
|**端口**|**传入/传出**|**协议**|**说明**|  
|135, 139, 445|传出|TCP|必需。|  
|137, 138|传出|UDP|必需。|  
|500, 4500|传出|UDP|如果你的域策略需要通过 IPSec 进行网络通信，则需要。|  
|80|传出|TCP|Web 服务器调试所必需。|  
  
## <a name="how-to-configure-ports-in-windows-firewall"></a>如何在 Windows 防火墙中配置端口  
  
1. 在“启动”  菜单中，搜索“高级安全 Windows 防火墙”  。  
  
2. 单击“入站规则”  或“出站规则”  ，然后单击“操作”  列表中的“新规则”  。  
  
3. 在“规则类型”  页上，选择“端口”  ，然后单击“下一步”  。  
  
4. 在“协议和端口”  页上，选择端口协议（TCP 或 UDP）。 选择“特定本地端口”  ，并输入你想要为协议启用的一个或多个端口号。 使用逗号分隔数字。 然后，单击 **“下一步”** 。  
  
5. 在“操作”  页上，选择“允许连接”  ，然后单击“下一步”  。  
  
6. 在“配置文件”  页上，选择要为端口启用的一个或多个网络类型。 你选择的类型必须包括远程计算机连接到的网络。 然后，单击 **“下一步”** 。  
  
7. 在“名称”  页上，键入规则的名称，然后单击“完成”  。  
  
8. 你应该会在“入站规则”  或“出站规则”  列表中看到你的新规则。  
  
## <a name="see-also"></a>请参阅  
 [远程调试](../debugger/remote-debugging.md)
