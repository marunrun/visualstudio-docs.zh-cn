---
title: 远程调试 C# 或 VB 项目 | Microsoft Docs
ms.custom:
- remotedebugging"=
- seodec18
ms.date: 08/14/2018
ms.topic: conceptual
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: a9753fbb-e7f4-47f0-9dbe-9de90c6c8457
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 5f147acae956ad380c6e85984de29d5316394c0a
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301073"
---
# <a name="remote-debugging-a-c-or-visual-basic-project-in-visual-studio"></a>在 Visual Studio 中远程调试 C# 或 Visual Basic 项目
若要调试已部署到另一台计算机上的 Visual Studio 应用程序，请在部署了应用的计算机上安装并运行远程工具，将项目配置为从 Visual Studio 连接到远程计算机，然后运行应用。

![远程调试器组件](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

如需详细了解如何远程调试通用 Windows 应用 (UWP)，请参阅[调试已安装的应用包](debug-installed-app-package.md)。

## <a name="requirements"></a>要求

Windows 7 和更高版本（非电话）以及从 Windows Server 2008 Service Pack 2 开始的 Windows Server 版本支持远程调试器。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

> [!NOTE]
> 不支持在通过代理连接的两台计算机之间进行调试。 不建议通过高延迟或低带宽连接（如拨号 Internet）或跨国家/地区的 Internet 进行调试，否则可能会导致调试失败或速度过慢。

## <a name="download-and-install-the-remote-tools"></a>下载和安装远程工具

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> 在某些情况下，从文件共享运行远程调试器可能是最有效的方法。 有关详细信息，请参阅[从文件共享运行远程调试器](../debugger/remote-debugging.md#fileshare_msvsmon)。

## <a name="set-up-the-remote-debugger"></a><a name="BKMK_setup"></a>设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果需要为其他用户添加权限，请更改远程调试器的身份验证模式或端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

## <a name="remote-debug-the-project"></a><a name="remote_csharp"></a> 远程调试项目
调试器不能将 Visual C# 或 Visual Basic 桌面应用程序部署到远程计算机，但你仍然可以按如下所示方法远程调试它们。 以下过程假定你希望在名为 MJO-DL 的计算机上调试它，如下图所示。

1. 创建一个名为“MyWpf”的 WPF 项目。

2. 在代码中的某个容易到达的地方设置断点。

    例如，可在按钮处理程序中设置断点。 若要执行此操作，请打开“MainWindow.xaml”并从“工具箱”中添加按钮控件，然后双击该按钮以打开其处理程序。

3. 在“解决方案资源管理器”中，右键单击项目，然后选择“属性”。

4. 在“属性”页上，选择"调试"选项卡 。

    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")

5. 请确保“工作目录”文本框为空。

6. 选择“使用远程计算机”，然后在文本框中键入“yourmachinename:port” 。 （端口号显示在远程调试器窗口中。 端口号在每个版本的 Visual Studio 中递增 2）。

    在此示例中，使用：
    ::: moniker range=">=vs-2019"
    Visual Studio 2019 上的 MJO-DL:4024
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 上的 MJO-DL:4022
    ::: moniker-end

7. 请确保未选中“启用本机代码调试”。

8. 生成项目。

9. 在远程计算机上创建一个文件夹，其路径与 Visual Studio 计算机上的调试文件夹相同：\<source path>\MyWPF\MyWPF\bin\Debug 。

10. 将你刚才从 Visual Studio 计算机生成的可执行文件复制到远程计算机上新创建的文件夹。

    > [!CAUTION]
    > 不要对代码进行更改或重新生成（否则必须重复此步骤）。 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。

    可手动复制项目，使用 Xcopy、Robocopy、Powershell 或其他选项。

11. 请确保远程调试器正在目标计算机上运行（如果没有，请在“开始”菜单中搜索“远程调试器”） 。 远程调试器窗口如下所示。

     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")

12. 在 Visual Studio 中，开始调试（单击“调试”>“启动调试”，或按 F5） 。

13. 如果出现提示，请输入网络凭据以连接到远程计算机。

     所需凭据因网络安全配置而异。 例如，在域计算机上，你可以输入域名和密码。 在非域计算机上，可以输入计算机名和有效用户帐户名（如 <strong>MJO-DL\name@something.com</strong>）以及正确的密码。

     应看到远程计算机上打开了 WPF 应用程序的主窗口。

14. 如有必要，请采取操作来命中断点。 你应看到该断点处于活动状态。 如果不是，则尚未加载应用程序的符号。 请重试，如果这不起作用，请在[了解符号文件和 Visual Studio 的符号设置](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)中获取有关加载符号以及如何对其进行故障排除的信息。

15. 在 Visual Studio 机器上，你应看到执行在断点处停止。

    如果具有任何需要由应用程序使用的非代码文件，则需要将其包含在 Visual Studio 项目中。 为其他文件创建项目文件夹（在“解决方案资源管理器”中，单击“添加”>“新建文件夹”） 。 然后将文件添加到文件夹（在“解决方案资源管理器”，单击“添加”>“现有项目”，然后选择文件） 。 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”  。

## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)