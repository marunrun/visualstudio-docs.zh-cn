---
title: 调试已安装的 UWP 应用包 | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.installedapppackagelauncher
- vs.debug.remote.connection
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- app package, debug
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 4bf9306ea1604d032ce9f4436759b11c4d17c343
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563154"
---
# <a name="debug-an-installed-uwp-app-package-in-visual-studio"></a>在 Visual Studio 中调试已安装的 UWP 应用包

Visual Studio 可以调试 Windows 10 计算机以及 Xbox、HoloLens 和 IoT 设备上已安装的通用 Windows 平台 (UWP) 应用包。

>[!NOTE]
>手机不支持 Visual Studio 调试已安装的 UWP 应用。

有关调试 UWP 应用的详细信息，请参阅博客文章上[调试已安装的应用包](https://devblogs.microsoft.com/devops/updates-for-debugging-installed-app-packages-in-visual-studio-2015-update-2/)并[构建通用 Windows 应用 (UWP)](https://devblogs.microsoft.com/visualstudio/universal-windows-apps-targeting-windows-10-anniversary-sdk/)。

## <a name="debug-an-installed-uwp-app-on-a-local-machine"></a>调试本地计算机上已安装的 UWP 应用

1. 在 Visual Studio 中，选择**调试** > **其他调试目标** > **调试安装的应用程序包**。

1. 在“调试已安装的应用包”对话框的“连接类型”下，选择“本地计算机”。

1. 在“已安装的应用包”下选择要调试的应用，或在搜索框中键入其名称。 未运行的已安装应用包显示在“未运行”下，正在运行的应用显示在“正在运行”下。

   ![DebugInstalledAppPackage](../debugger/media/debug-installed-app-pkg.png "DebugInstalledAppPackage")

1. 如有必要，更改“调试此代码类型”下的代码类型，然后选择其他选项。
   - 选择“不启动，但在启动时调试我的代码”，在应用启动时开始调试。 应用启动时开始调试是调试来自[不同启动方法](/windows/uwp/xbox-apps/automate-launching-uwp-apps)（例如使用自定义参数激活协议）的控制路径的有效方法。

1. 选择“开始”，或如果应用正在运行，则选择“附加”。

> [!NOTE]
> 此外，还可以通过在 Visual Studio 中选择“调试” > “附加到进程”以附加到任何正在运行的 UWP 或其他应用进程。 无需原始 Visual Studio 项目也可附加到正在运行的进程中，但是在调试你没有原始代码的进程时，加载应用的符号会有很大帮助。 请参阅[在调试器中指定符号和源文件](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="remote"></a> 调试远程计算机或设备上已安装的 UWP 应用

Visual Studio 首次调试 Windows 10 设备或后创意者更新 Windows 10 远程计算机上已安装的 UWP 应用时，会在目标设备上安装远程调试工具。

1. 在 Visual Studio 计算机和远程设备/计算机上[启用开发人员模式](/windows/uwp/get-started/enable-your-device-for-development)。

1. 如果要连接到运行预创意者更新 Windows 10 的远程计算机，请在该远程计算机上[手动安装并启动远程调试器](../debugger/remote-debugging.md)。

1. 在 Visual Studio 计算机上，选择“调试” > “其他调试目标” > “调试已安装的应用包”。

1. 在“调试已安装的应用包”对话框的“连接类型”下，选择“远程计算机”或“设备”。

   如果选择**设备**，计算机必须以物理方式连接到 Windows 10 设备。

   对于远程计算机，如果计算机地址未出现在“地址”旁，请选择“更改”。

   1. 在中**远程连接**对话框旁边**地址**，键入名称或你想要连接到计算机的 IP 地址。

      ![ChooseRemoteComputer](../debugger/media/debug-remote-app-pkg.png "ChooseRemoteComputer")

      如果调试器无法连接到远程计算机使用的计算机名称，请改为使用的 IP 地址。 用于 Xbox、 HoloLens 或 IoT 设备的 IP 地址。
   1. 选择一个身份验证选项旁边**身份验证模式**。

      对于大多数应用中，保留默认值**通用 （未加密的协议）**。
   1. 选择**选择**。

1. 在“已安装的应用包”下选择要调试的应用，或在搜索框中键入其名称。 未运行的已安装应用包显示在“未运行”下，正在运行的应用显示在“正在运行”下。

1. 如有必要，更改“调试此代码类型”下的代码类型，然后选择其他选项。
   - 选择“不启动，但在启动时调试我的代码”，在应用启动时开始调试。 应用启动时开始调试是调试来自[不同启动方法](/windows/uwp/xbox-apps/automate-launching-uwp-apps)（例如使用自定义参数激活协议）的控制路径的有效方法。

1. 选择“开始”，或如果应用正在运行，则选择“附加”。

首次开始调试已连接的 Xbox、HoloLens 或 IoT 设备上已安装的应用包时，Visual Studio 会对目标设备安装正确版本的远程调试器。 安装远程调试器可能需要一些时间，并且在安装过程中会显示“正在启动远程调试器”消息。

>[!NOTE]
>目前，Xbox 或 HoloLens 设备附加调试器时，如果已运行则重启应用。

对于UWP 应用远程部署的更多信息，请参阅[部署和调试 UWP 应用](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)并[远程计算机上的调试 UWP 应用](run-windows-store-apps-on-a-remote-machine.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.md)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [远程调试](../debugger/remote-debugging.md)
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)