---
title: 远程调试C#或 VB 项目 |Microsoft Docs
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
ms.openlocfilehash: 4c646f8f6dc228d42d6efb5ec44f3ec19a53a551
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408533"
---
# <a name="remote-debugging-a-c-or-visual-basic-project-in-visual-studio"></a>远程调试 Visual Studio 中的 C# 或 Visual Basic 项目
若要调试已部署在另一台计算机的 Visual Studio 应用程序，安装和在其中部署您的应用程序的计算机上运行远程工具、 将项目配置为从 Visual Studio 中，连接到远程计算机，然后运行应用。

![远程调试器组件](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

有关远程调试通用 Windows 应用 (UWP) 的信息，请参阅[调试安装的应用程序包](debug-installed-app-package.md)。

## <a name="requirements"></a>要求

远程调试器是在 Windows 7 上受支持和更高版本 (不 phone) 和从 Windows Server 2008 Service Pack 2 的 Windows Server 的版本。 有关要求的完整列表，请参阅[要求](../debugger/remote-debugging.md#requirements_msvsmon)。

> [!NOTE]
> 不支持调试通过代理连接的两台计算机之间。 调试通过高延迟或低带宽连接，例如拨号 Internet，或通过 Internet 跨国家/地区不建议并可能会失败或很令人无法接受慢。

## <a name="download-and-install-the-remote-tools"></a>下载和安装远程工具

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> 在某些情况下，它可以是最有效，若要从文件共享运行远程调试器。 有关详细信息，请参阅[从文件共享运行远程调试器](../debugger/remote-debugging.md#fileshare_msvsmon)。

## <a name="BKMK_setup"></a>设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 如果您需要添加其他用户的权限更改身份验证模式，或者远程调试器的端口号，请参阅[配置远程调试器](../debugger/remote-debugging.md#configure_msvsmon)。

## <a name="remote_csharp"></a> 远程调试项目
调试器不能将 Visual C# 或 Visual Basic 桌面应用程序部署到远程计算机，但你仍然可以按如下所示方法远程调试它们。 以下过程假设你想要在名为的计算机上调试它**MJO DL**下, 图中所示。

1. 创建一个名为“MyWpf”的 WPF 项目。

2. 在代码中的某个容易到达的地方设置断点。

    例如，可在按钮处理程序中设置断点。 若要执行此操作，打开 MainWindow.xaml，然后添加一个按钮控件从工具箱中，双击按钮以打开它的处理程序。

3. 在解决方案资源管理器，右键单击该项目并选择**属性**。

4. 在“属性”页上，选择"调试"选项卡。

    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")

5. 请确保“工作目录”文本框为空。

6. 选择**使用远程计算机**，然后键入**yourmachinename:port**在文本框中。 （远程调试器窗口中显示的端口号。 端口号递增每个版本的 Visual Studio 中的 2）。

    在此示例中，使用：
    ::: moniker range=">=vs-2019"
    **MJO-DL:4024**于 Visual Studio 2019
    ::: moniker-end
    ::: moniker range="vs-2017"
    **MJO-DL:4022** Visual Studio 2017
    ::: moniker-end

7. 请确保未选中“启用本机代码调试”。

8. 生成项目。

9. 在远程计算机上创建一个文件夹，其路径与 Visual Studio 计算机上的调试文件夹相同：\<source path>\MyWPF\MyWPF\bin\Debug。

10. 将你刚才从 Visual Studio 计算机生成的可执行文件复制到远程计算机上新创建的文件夹。

    > [!CAUTION]
    > 对代码或重新生成不会进行任何更改 （或必须重复此步骤）。 复制到远程计算机的可执行文件必须与你的本地源和符号完全匹配。

    可以手动复制该项目，使用 Xcopy、 Robocopy、 Powershell 或其他选项。

11. 请确保在目标计算机上正在运行远程调试器 (如果不是，搜索**远程调试器**中**启动**菜单)。 远程调试器窗口外观如下所示。

     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")

12. 在 Visual Studio 中，开始调试（单击“调试”>“启动调试”，或按 F5）。

13. 如果系统提示，请输入网络凭据以连接到远程计算机。

     所需的凭据会有所不同，具体取决于网络的安全配置。 例如，在域的计算机，可以输入你的域名和密码。 在非域计算机上，你可能会输入计算机名称和有效的用户帐户名称，如<strong>MJO-DL\name@something.com</strong>，以及正确的密码。

     应看到远程计算机上打开了 WPF 应用程序的主窗口。

14. 如果有必要，请采取措施以命中断点。 你应看到该断点处于活动状态。 如果不是，则尚未加载应用程序的符号。 重试，并且如果这不起作用，获取有关加载符号的信息和如何解决在这些问题[了解符号文件和 Visual Studio 的符号设置](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)。

15. 在 Visual Studio 机器上，你应看到执行在断点处停止。

    如果有需要应用程序使用任何非代码文件，您需要将其包含在 Visual Studio 项目。 为其他文件创建项目文件夹（在“解决方案资源管理器”中，单击“添加”>“新建文件夹”）。 然后将文件添加到文件夹（在“解决方案资源管理器”，单击“添加”>“现有项目”，然后选择文件）。 在每个文件的“属性”页中，将“复制到输出目录”设置为“始终复制”。

## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.md)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)