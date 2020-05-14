---
title: 启动应用商店应用 （JavaScript） 的调试会话 |微软文档
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.installedapppackagelauncher
- vs.debug.error.wwahost_scriptdebuggingdisabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: fb91203f-2cf4-44d3-8ed9-93bc5aaa50b8
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4b4e861c8985ee37a8c2d9b7f9286d6284bb4f91
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301379"
---
# <a name="start-a-debugging-session-for-store-apps-in-visual-studio-javascript"></a>在 Visual Studio 中为应用商店应用启动调试会话 (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 和 Windows 电话*（./图像/windows_and_phone_content.png"windows_and_phone_content"）

 本主题介绍如何针对用 JavaScript 和 HTML5 编写的 Windows 应用商店应用启动调试会话。 你可以使用单个按键启动调试，或者你可以为特定的场景配置调试会话，然后选择启动应用的方式。

> [!NOTE]
> 对于以 XAML 和可视化 C#、可视C++或可视化基本编写的应用，请参阅[启动调试会话（VB、C#、C++和 XAML）](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a>在本主题中
 [在本主题中](#BKMK_In_this_topic)

 [启动调试的简单方法](#BKMK_The_easy_way_to_start_debugging)

 [配置调试会话](#BKMK_Configure_the_debugging_session)

- [打开项目的调试属性页](#BKMK_Open_the_debugging_property_page_for_the_project)

- [选择生成配置选项](#BKMK_Choose_the_build_configuration_options)

- [选择部署目标](#BKMK_Choose_the_deployment_target)

- [选择要使用的调试器](#BKMK_Choose_the_debugger_to_use)

- [（可选）推迟启动调试会话中的应用](#BKMK__Optional__Delay_starting_app_in_the_debug_session)

- [（可选）禁用网络环回](#BKMK__Optional__Disable_network_loopbacks)

  [启动调试会话](#BKMK_Start_the_debugging_session)

- [启动调试 (F5)](#BKMK_Start_debugging__F5_)

- [启动调试 (F5)，但推迟启动应用程序](#BKMK_Start_debugging__F5__but_delay_the_app_start)

  [在调试器中启动已安装的应用程序](#BKMK_Start_an_installed_app_in_the_debugger)

  [将调试器附加到正在运行的应用程序](#BKMK_Attach_the_debugger_to_a_running_app_)

- [将应用程序设置为以调试模式运行](#BKMK_Set_the_app_to_run_in_debug_mode)

- [附加调试器](#BKMK_Attach_the_debugger)

## <a name="the-easy-way-to-start-debugging"></a><a name="BKMK_The_easy_way_to_start_debugging"></a>开始调试的简单方法
 ![仅适用于 Windows](../debugger/media/windows-only-content.png "windows_only_content")

1. 在 Visual Studio 中打开应用程序解决方案。

2. 如果解决方案同时包含 Windows 应用商店和 Windows Phone 应用商店应用的项目，请确保要调试的项目是启动项目。 在"解决方案浏览"中，选择项目，然后从上下文菜单**中选择"设置为启动项目**"。

3. 按 F5。

   ![仅适用于 Windows Phone](../debugger/media/phone-only-content.png "phone_only_content")

   Visual Studio 生成并启动附有调试器的应用程序。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。 有关详细信息，请参阅[快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)。

## <a name="configure-the-debugging-session"></a><a name="BKMK_Configure_the_debugging_session"></a>配置调试会话
 由于脚本未编译，不会应用生成配置和平台设置。 如果要调试C++或托管组件，请将 **"配置"** 设置为**调试**，并从 **"配置"** 对话框中选择目标平台。

### <a name="open-the-debugging-property-page-for-the-project"></a><a name="BKMK_Open_the_debugging_property_page_for_the_project"></a>打开项目的调试属性页

1. 在解决方案资源管理器中选择项目。 在快捷菜单中，选择 **“属性”**。

2. 展开**配置属性**节点，然后选择 **"调试"**

### <a name="choose-the-build-configuration-options"></a><a name="BKMK_Choose_the_build_configuration_options"></a>选择生成配置选项

1. 从 **“配置”** 列表中，选择 **“调试”** 或 **“(活动)调试”**。

2. 从 **“平台”** 列表中选择要生成的目标平台。 在大多数情况下，任何**CPU**都是最佳选择。

### <a name="choose-the-deployment-target"></a><a name="BKMK_Choose_the_deployment_target"></a>选择部署目标
 可在 Visual Studio 计算机上、本地计算机上的 Visual Studio 模拟器中或远程计算机上部署和调试应用。 您可以从**调试器**中选择目标以在项目的 **"调试"** 属性页上启动列表。

 ![仅适用于 Windows](../debugger/media/windows-only-content.png "windows_only_content")

 对于 Windows 应用商店应用，请从 **"目标"设备**列表中选择以下选项之一：

|||
|-|-|
|**本地机器**|在本地计算机上的当前会话中调试应用程序。 请参阅[在本地计算机上运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-the-local-machine.md)。|
|**模拟**|在 Visual Studio 的 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 应用程序模拟器中调试应用程序。 模拟器是一个桌面窗口，在该窗口中可调试本地计算机上未提供的设备功能，如触摸手势和设备旋转。 请参阅[在模拟器中运行 Windows 应用商店应用](../debugger/run-windows-store-apps-in-the-simulator.md)。|
|**远程计算机**|在通过 Intranet 连接到本地计算机或使用以太网电缆直接连接到本地计算机的设备上调试应用程序。 若要进行远程调试，必须安装 Visual Studio 远程工具，并且远程设备上必须正在运行这些工具。 请参阅[在远程计算机上运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。|

 如果选择 **“远程计算机”**，则按以下某种方式指定远程计算机的名称或 IP 地址：

- 在 **"计算机名称"** 框中输入远程计算机的名称或 IP 地址。

- 选择 **"计算机名称"** 框中的向下箭头，然后选择**\<"查找...">**。 然后从 **"选择远程调试器连接"** 对话框中选择远程计算机。

   ![选择远程调试器连接](../debugger/media/vsrun-pro-selectremotedebuggerdlg.png "VSRUN_PRO_SelectRemoteDebuggerDlg")

  > [!NOTE]
  > “选择远程调试器连接”对话框显示本地子网上的计算机以及通过以太网电缆直接连接到 Visual Studio 计算机的计算机。 若要指定其他计算机，请在 **“计算机名称”** 框中输入名称。

  ![仅适用于 Windows Phone](../debugger/media/phone-only-content.png "phone_only_content")

  对于 Windows 应用商店电话应用，从 **"目标"设备**列表中选择**设备**或其中一个仿真器。

### <a name="choose-the-debugger-to-use"></a><a name="BKMK_Choose_the_debugger_to_use"></a>选择要使用的调试器
 默认情况下，调试器附加到你应用中的 JavaScript 代码。 你可以选择调试应用组件的本机 C++ 和托管代码，而不是 JavaScript 代码。 在应用程序项目的 **“调试”** 属性页上 **“调试器类型”** 列表中指定要调试的代码。

 从**调试器类型**列表中选择这些调试器之一：

|||
|-|-|
|**仅限脚本**|调试应用程序中的 JavaScript 代码。 忽略托管代码和本机代码。|
|**仅限本机**|调试应用程序中的本机 C/C++ 代码。 忽略托管代码和 JavaScript 代码。|
|**带脚本的本机**|调试应用中的本机 C++ 代码和 JavaScript 代码。|
|**仅限托管**|调试应用程序中的托管代码。 忽略 JavaScript 代码和本机 C/C++ 代码。|
|**混合(托管和本机)**|调试应用程序中的本机 C/C++ 代码和托管代码。 忽略 JavaScript 代码。|

### <a name="optional-delay-starting-the-app-in-the-debug-session"></a><a name="BKMK__Optional__Delay_starting_app_in_the_debug_session"></a>（可选）延迟在调试会话中启动应用
 默认情况下，启动调试后，Visual Studio 将立即启动应用程序。 也可启动调试会话但推迟启动应用程序。 从“开始”菜单或由激活协定启动应用时或者由其他进程或方法启动应用时，将在调试器中启动应用。 你也可以使用延迟的启动在应用未运行时，在应用中调试你希望执行的后台事件。

 在应用项目的 **"调试**"属性页上的 **"启动应用程序**"列表中指定是否延迟应用的启动。 选择以下选项之一：

- 选择 **"否**"可延迟应用的启动。

- 选择 **"是**"可立即启动应用。

### <a name="optional-disable-network-loopbacks"></a><a name="BKMK__Optional__Disable_network_loopbacks"></a>（可选）禁用网络环回
 ![仅适用于 Windows](../debugger/media/windows-only-content.png "windows_only_content")

 为安全起见，不允许以标准方式安装的 Windows 应用商店应用程序对装有它的设备进行网络调用。 默认情况下，Visual Studio 部署功能为所部署的应用程序创建此规则的例外。 通过此例外，在一台计算机上即可测试通信过程。 向 Window 应用商店提交应用程序之前，应在没有例外的情况下测试应用程序。

 要删除网络环回豁免，请从 **"调试**属性"页上的 **"允许网络环回**"列表中选择 **"否**"。

## <a name="start-the-debugging-session"></a><a name="BKMK_Start_the_debugging_session"></a>启动调试会话

### <a name="start-debugging-f5"></a><a name="BKMK_Start_debugging__F5_"></a>开始调试 （F5）
 当您在**调试**菜单（键盘：F5）中选择 **"开始调试"** 时，Visual Studio 会启动应用，并附加调试器。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

### <a name="start-debugging-f5-but-delay-the-app-start"></a><a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a>开始调试 （F5），但延迟应用启动
 你可以将应用设置为在调试模式中运行，但通过调试器之外的方法启动应用。 例如，你可能需要调试从“开始”菜单进行的应用程序启动，或在不启动应用程序的情况下调试应用程序中的后台进程。若要延迟应用程序启动，请执行下列操作：

1. 在应用项目属性的**调试**页上，从**启动应用程序**列表中选择 **"否**"。

2. 在**调试**菜单上选择 **"开始调试**"（键盘：F5）。

3. 从“开始”菜单、执行协定或由其他过程启动应用程序。

   随后应用程序在调试模式下启动。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

   . 有关调试后台任务的详细信息，请参阅[Windows 应用商店的触发器挂起、恢复和后台事件。](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)

## <a name="start-an-installed-app-in-the-debugger"></a><a name="BKMK_Start_an_installed_app_in_the_debugger"></a>在调试器中启动已安装的应用
 在使用 F5 启动调试时，Visual Studio 会生成并部署应用程序，将应用程序设置为在调试模式中运行，然后启动应用程序。 若要启动设备上已安装的应用程序，请使用“调试安装的应用程序包”对话框。 在需要调试已从 Windows 应用商店安装的应用程序时，或在具有应用程序的源文件但没有针对应用程序的 Visual Studio 项目时，此过程非常有用。 例如，你的自定义生成系统可能不使用 Visual Studio 项目或解决方案。

 应用程序可安装在本地设备上，也可安装在远程设备上。  你可以立即启动应用程序，或将应用程序设置为当其通过其他进程或方法（如从“开始”菜单或通过激活协定）启动时在调试器中运行，也可以将应用程序设置为当需要在未启动应用程序的情况下调试后台进程时在调试模式中运行。 有关详细信息，请参阅为[Windows 应用商店触发挂起、恢复和后台事件）。](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)

 若要将已安装的应用程序设置为在调试模式中运行，请执行下列操作：

> [!NOTE]
> 在你启动此过程时，应用程序不得运行。

1. 在 **“调试”** 菜单上，选择 **“调试安装的应用程序包”**

2. 请从列表中选择下列选项之一：

   |                    |                                                                                                                                                                                                                                                                                                                                                                                                           |
   |--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **本地机器**  |                                                                                                                在本地计算机上的当前会话中调试应用程序。 请参阅[在本地计算机上运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-the-local-machine.md)。                                                                                                                 |
   |   **模拟**    | 在 Visual Studio 的 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 应用程序模拟器中调试应用程序。 模拟器是一个桌面窗口，在该窗口中可调试本地计算机上未提供的设备功能，如触摸手势和设备旋转。 请参阅[在模拟器中运行 Windows 应用商店应用](../debugger/run-windows-store-apps-in-the-simulator.md)。 |
   | **远程计算机** |                          在通过 Intranet 连接到本地计算机或使用以太网电缆直接连接到本地计算机的设备上调试应用程序。 若要进行远程调试，必须安装 Visual Studio 远程工具，并且远程设备上必须正在运行这些工具。 请参阅[在远程计算机上运行 Windows 应用商店应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。                           |

3. 从 **“安装的应用程序包”** 列表中选择应用程序。

4. 从 **“调试此代码类型”** 列表中选择要使用的调试引擎。

5. （可选）。 选择 **“不启动，但在启动时调试代码”** 以在通过其他某种方法启动应用程序时调试应用程序或调试后台进程。

   在单击 **“启动”** 时，应用程序将启动或设置为在调试模式中运行。

## <a name="attach-the-debugger-to-a-running-app"></a><a name="BKMK_Attach_the_debugger_to_a_running_app_"></a>将调试器附加到正在运行的应用
 若要将调试器附加到 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 应用程序，必须使用可调式包管理器将应用程序设置为以调试模式运行。 可调式包管理器与 Visual Studio 远程工具一并安装。

 当需要调试已安装的应用（如从 Windows 应用商店安装的应用）时，将调试器附加到应用很有用。 在拥有应用程序的源文件，但没有应用程序的 Visual Studio 项目时，必须进行附加。 例如，你的自定义生成系统可能不使用 Visual Studio 项目或解决方案。

 附加到应用：

1. 将应用程序设置为以调试模式运行。 必须在应用程序未运行时执行此操作。

2. 启动应用。 可从“开始”菜单、执行协定或通过某些其他方法启动该应用。

3. 将调试器附加到正在运行的应用程序。

### <a name="set-the-app-to-run-in-debug-mode"></a><a name="BKMK_Set_the_app_to_run_in_debug_mode"></a>将应用设置为在调试模式下运行

1. 在装有该应用程序的设备上安装 Visual Studio 远程工具。 请参阅[安装远程工具](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx#BKMK_Installing_the_Remote_Tools)。

2. 在“开始”菜单上，搜索 `Debuggable Package Manager`，然后启动它。

     随后显示 PowerShell 窗口，该窗口针对 AppxDebug cmdlet 进行了正确的配置。

3. 若要能够调试应用程序，必须指定该应用程序的 PackageFullName 标识符。 若要查看包含 PackageFullName 的所有应用程序的列表，请在 PowerShell 提示符下键入 `Get-AppxPackage` 。

4. 在 PowerShell 提示符下，输入 `Enable-AppxDebug` *PackageFullName* ，其中 *PackageFullName* 是应用的 PackageFullName 标识符。

### <a name="attach-the-debugger"></a><a name="BKMK_Attach_the_debugger"></a>附加调试器

> [!TIP]
> JavaScript 应用使用 wwahost.exe 进程的实例运行。 附加到应用时，如果其他 JavaScript 应用正在运行，你将需要了解应用正在运行的 wwahost.exe 的数字进程 ID (PID)。
>
> 处理此情形的最简单方法是关闭所有其他 JavaScript 应用。 否则，你可以在启动应用之前打开 Windows 任务管理器并记下 wwahost.exe 进程的 ID。 在"**可用进程"** 对话框中指定要附加到的进程时，应用的 wwahost.exe 将具有与您已注意到的 ID 不同的 ID。

 若要附加调试器，请执行以下操作：

1. 在 **“调试”** 菜单上选择 **“附加到进程”**。

    出现 **“附加到进程”** 对话框。

2. 若要附加到远程设备上的应用程序，请在 **“限定符”** 框中指定该远程设备。 可以：

   - 在 **“限定符”** 框中输入名称。

   - 选择 **"限定符"** 框中的向下箭头，然后从以前连接的设备列表中选择设备。

   - 选择 **"查找"** 可从本地子网上的设备列表中选择设备。

3. 在 **“附加到”** 框中指定要调试的代码类型。

    选择 **“选择”** ，然后执行下列操作之一：

   - 选中 **“自动确定要调试的代码类型”**

   - 选中 **“调试以下代码类型”** ，然后从列表中选择一个或多个类型。

4. 在 **"可用进程"** 列表中，选择相应的**wwahost.exe**进程。 使用 **"标题"** 列标识应用。

5. 选择 **“附加”**。

   Visual Studio 将调试器附加到该进程。 持续执行至抵达某个断点、手动暂停执行、发生无法处理的异常或应用程序结束为止。

## <a name="see-also"></a>另请参阅
 [在调试会话 （JavaScript） 快速入门中控制执行](../debugger/control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript.md)[：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md) [触发器挂起、恢复和后台事件，在](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)[可视化工作室中调试应用](../debugger/debug-store-apps-in-visual-studio.md)
