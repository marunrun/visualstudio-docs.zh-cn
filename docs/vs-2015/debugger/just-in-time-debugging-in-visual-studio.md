---
title: 实时调试
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
- CSharp
- VB
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
ms.assetid: 14972d5f-69bc-479b-9529-03b8787b118f
caps.latest.revision: 51
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ad2814dffa75809a318dc7cebe7831b5ecec7d29
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690596"
---
# <a name="just-in-time-debugging-in-visual-studio"></a>在 Visual Studio 进行实时调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当在 Visual Studio 外运行的应用程序中发生异常或崩溃时，实时调试会自动启动 Visual Studio。 这使你能够在 Visual Studio 未运行时测试应用程序，并在出现问题时开始使用 Visual Studio 进行调试。

实时调试适用于 Windows 桌面应用。 它不适用于 Windows 通用应用，并且不适用于在本机应用程序中承载的托管代码，如可视化工具。

## <a name="did-the-just-in-time-debugger-dialog-box-appear-when-trying-to-run-an-app"></a><a name="BKMK_Scenario"></a> 尝试运行应用时是否显示 "实时调试器" 对话框？

当你看到 "Visual Studio 实时调试器" 对话框时，你应执行的操作取决于你要执行的操作：

#### <a name="if-you-want-to-get-rid-of-the-dialog-box-and-just-run-the-app-normally"></a>如果要去掉对话框并正常运行应用程序，请执行

1.  (高级用户) 如果已安装 Visual Studio (或者之前已将其删除) ，请 [禁用实时调试](#BKMK_Enabling) ，并再次尝试运行应用。

2. 如果在 Internet Explorer 中运行 web 应用，请禁用脚本调试。

    在 "Internet 选项" 对话框中禁用脚本调试。 你可以从 "**控制面板**" "  /  **网络和 internet**" 选项中访问它  /  **Internet Options** (具体步骤取决于你的 Windows 和 internet Explorer) 的版本。

    ![JITInternetOptions](../debugger/media/jitinternetoptions.png "JITInternetOptions")

3. 重新打开出现错误的网页。 如果这不能解决问题，请与 web 应用的所有者联系以解决问题。

4. 如果你运行的是另一种类型的 Windows 应用，则需要与应用的所有者联系以修复错误，然后重新安装应用的固定版本。

#### <a name="if-you-want-to-fix-or-debug-the-error-advanced-users"></a>如果要修复或调试错误 (高级用户) 

- 您必须 [安装 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) 才能查看有关错误的详细信息并尝试对其进行调试。 有关详细说明，请参阅 [使用 JIT](#BKMK_Using_JIT) 。 如果无法解决此错误并修复应用程序，请与应用程序的所有者联系以解决此错误。

## <a name="enable-or-disable-just-in-time-debugging"></a><a name="BKMK_Enabling"></a> 启用或禁用实时调试
 你可以从 Visual Studio 的 " **工具/选项** " 对话框中启用或禁用实时调试。

#### <a name="to-enable-or-disable-just-in-time-debugging"></a>启用或禁用实时调试

1. 打开 Visual Studio 在“工具”  菜单上，单击“选项” 。

2. 在 " **选项** " 对话框中，选择 " **调试** " 文件夹。

3. 在 "**调试**" 文件夹中，选择 **"实时" 页。**

4. 在 " **启用这些代码类型的实时调试** " 框中，选择或清除相关的程序类型： " **托管**"、" **本机**" 或 " **脚本**"。

    要在启用实时调试后禁用它，必须使用管理员特权运行。 启用实时调试会设置一个注册表项，需要管理员特权才可以更改该项。

5. 单击“确定”。

   即便计算机中不再安装有 Visual Studio，仍可启用实时调试。 未安装 Visual Studio 时，无法从 Visual Studio 的 " **选项** " 对话框中禁用实时调试。 对于这种情况，你可以通过编辑 Windows 注册表来禁用实时调试。

#### <a name="to-disable-just-in-time-debugging-by-editing-the-registry"></a>通过编辑注册表禁用实时调试

1. 在 " **开始** " 菜单上，搜索并运行 `regedit.exe`

2. 在 " **注册表编辑器** " 窗口中，找到并删除以下注册表项：

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger

3. 如果计算机运行的是64位操作系统，还请删除以下注册表项：

    - HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger

    - HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger

4. 注意不要意外删除或更改任何其他注册表项。

5. 关闭“注册表编辑器”窗口。

> [!NOTE]
> 如果尝试对服务器端应用禁用实时调试，并且这些步骤不能解决问题，请在 IIS 应用程序设置中关闭服务器端调试，然后重试。

#### <a name="to-enable-just-in-time-debugging-of-a-windows-form"></a>为 Windows 窗体启用实时调试

1. 默认情况下，Windows 窗体应用程序有一个顶级的异常处理程序，该处理程序允许程序在能够恢复时继续运行。 例如，如果 Windows 窗体应用程序引发了未处理的异常，则会看到如下所示的对话框：

     ![WindowsFormsUnhandledException](../debugger/media/windowsformsunhandledexception.png "WindowsFormsUnhandledException")

     若要启用对 Windows 窗体应用程序的实时调试，您必须执行以下附加步骤：

2. `jitDebugging` `true` 在 `system.windows.form` machine.config 或.exe.config 文件的部分中将值设置为 *\<application name>* ：

    ```
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```

3. 在 C++ Windows 窗体应用程序中，还必须在 .config 文件或你的代码中设置 `DebuggableAttribute`。 如果使用 [/Zi](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8) 而不使用 [/Og](https://msdn.microsoft.com/library/d10630cc-b9cf-4e97-bde3-8d7ee79e9435) 进行编译，则编译器会替你设置此属性。 然而，如果你想要调试非优化发布版本，则必须自行设置此项。 为此，你可以在应用程序的 AssemblyInfo.cpp 文件中添加下面一行：

    ```
    [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
    ```

     有关详细信息，请参阅 <xref:System.Diagnostics.DebuggableAttribute>。

## <a name="a-namebkmk_using_jituse-just-in-time-debugging"></a><a name="BKMK_Using_JIT">使用实时调试
 本部分说明当可执行文件引发异常时会发生的情况。

 必须安装 Visual Studio，才能按照以下步骤操作。 如果没有 Visual Studio，可以下载免费的 [Visual studio 2015 社区版](https://visualstudio.microsoft.com/vs/older-downloads/)。

 默认情况下，安装 Visual Studio 时会启用实时调试。

 出于本部分的目的，我们将在 Visual Studio 中创建一个引发的 c # 控制台应用程序 <xref:System.NullReferenceException> 。

 在 Visual Studio 中，创建名为**ThrowsNullException**的 c # 控制台应用 (**文件/新建/项目/Visual c #/console 应用程序**) 。 有关在 Visual Studio 中创建项目的详细信息，请参阅 [演练：创建简单的应用程序](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)。

 在 Visual Studio 中打开项目时，请打开 Program.cs 文件。 将 Main() 方法替换为以下代码，该代码会在控制台中打印一行，然后引发 NullReferenceException：

```csharp
static void Main(string[] args)
{
    Console.WriteLine("we will now throw a NullReferenceException");
    throw new NullReferenceException("this is the exception thrown by the console app");
}
```

> [!IMPORTANT]
> 为了使此过程在 [发布配置](../debugger/how-to-set-debug-and-release-configurations.md)中工作，需要关闭 [仅我的代码](../debugger/just-my-code.md)。 在 Visual Studio 中，单击 " **工具"/"选项**"。 在 " **选项** " 对话框中，选择 " **调试**"。 从 **启用仅我的代码**中删除检查。

 在 Visual Studio 中生成解决方案 (，选择 " **生成/重新生成解决方案** ") 。 您可以选择 "调试" 或 "发布" 配置。 有关生成配置的详细信息，请参阅 [了解生成配置](../ide/understanding-build-configurations.md)。

 生成过程将创建一个可执行的 ThrowsNullException.exe。 您可以在创建 c # 项目的文件夹下找到它： **. ..\ThrowsNullException\ThrowsNullException\bin\Debug** 或 **. ..\ThrowsNullException\ThrowsNullException\bin\Release**。

 双击 ThrowsNullException.exe。 应会看到如下所示的命令窗口：

 ![ThrowsNullExceptionConsole](../debugger/media/throwsnullexceptionconsole.png "ThrowsNullExceptionConsole")

 几秒钟后，将显示一个错误窗口：

 ![ThrowsNullExceptionError](../debugger/media/throwsnullexceptionerror.png "ThrowsNullExceptionError")

 不要单击 " **取消**！ 几秒钟后，应会看到两个按钮： " **调试** " 和 " **关闭程序**"。 单击 " **调试**"。

> [!CAUTION]
> 如果你的应用程序包含不受信任的代码，则会出现一个包含安全警告的对话框。 此对话框使可以决定是否继续调试。 在继续调试之前，请决定你是否信任相应代码。 代码是否为自己编写的？ 你是否信任代码编写者？ 如果应用程序在远程计算机上运行，你能否识别进程的名称？ 即便该应用程序在本地运行，也不一定表示它是可信的应用程序。 请考虑在您的计算机上运行恶意代码的可能性。 如果决定要调试的代码是可信代码，请单击 " **调试**"。 否则，请单击 " **不调试**"。

 此时将显示 " **Visual Studio 实时调试器** " 窗口：

 ![JustInTimeDialog](../debugger/media/justintimedialog.png "JustInTimeDialog")

 在 " **可能的调试器**" 下，应会看到 "Microsoft Visual Studio 2015 行" 的 **新实例** 处于选中状态。 如果尚未选择该选项，请立即选择它。

 在窗口底部的 " **是否要使用所选调试器进行调试？**" 下，单击 **"是"**。

 ThrowsNullException 项目在 Visual Studio 的新实例中打开，并在引发异常的行处停止执行：

 ![NullReferenceSecondInstance](../debugger/media/nullreferencesecondinstance.png "NullReferenceSecondInstance")

 可以从此时开始调试。 如果这是真正的应用程序，则需要找出代码引发异常的原因。

## <a name="just-in-time-debugging-errors"></a>实时调试错误
 如果程序崩溃时未看到该对话框，这可能是因为 Windows 错误报告计算机上的设置。 有关详细信息，请参阅 [。WER 设置](https://msdn.microsoft.com/library/windows/desktop/bb513638\(v=vs.85\).aspx)。

 你可能会遇到与实时调试相关联的下列错误消息。

- **无法附加到崩溃进程。指定的程序不是 Windows 或 MS-DOS 程序。**

     当你尝试附加到作为另一个用户运行的进程时，将发生此错误。

     若要解决此问题，请启动 Visual Studio，从 "**调试**" 菜单中打开 "**附加到进程**" 对话框，然后在 "**可用进程**" 列表中找到要调试的进程。 如果不知道进程名称，请查看 " **Visual Studio 实时调试器** " 对话框并记下进程 ID。 在 " **可用进程** " 列表中选择进程，然后单击 " **附加**"。 在 " **Visual Studio 实时调试器** " 对话框中，单击 " **否** " 以关闭该对话框。

- **未能启动调试器，因为没有用户登录。**

     在没有用户登录到控制台的计算机中，如果实时调试尝试启动 Visual Studio，则会发生此错误。 因为没有用户登录，所以没有用户会话来显示“实时调试”对话框。

     要解决此问题，请登录到计算机。

- **类没有注册。**

     此错误指出：调试器尝试创建一个可能是因为安装问题而没有注册的 COM 类。

     若要解决此问题，请使用安装盘重新安装或修复 Visual Studio 安装。

## <a name="see-also"></a>另请参阅
 [调试器安全](../debugger/debugger-security.md)[调试器基础知识](../debugger/debugger-basics.md)[实时，调试，"选项" 对话框](../debugger/just-in-time-debugging-options-dialog-box.md)[安全警告：附加到不受信任的用户所拥有的进程可能很危险。如果以下信息看上去可疑或无法确定，请不要附加到此进程](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015)
