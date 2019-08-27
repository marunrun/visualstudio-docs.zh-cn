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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690596"
---
# <a name="just-in-time-debugging-in-visual-studio"></a>在 Visual Studio 进行实时调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在实时调试 Visual Studio 会自动启动 Visual Studio 之外运行的应用程序中发生异常或崩溃时。 这使您测试应用程序，如果未运行 Visual Studio，并开始使用 Visual Studio 进行调试时出现问题。

实时调试适用于 Windows 桌面应用。 它并不适用于 Windows 通用应用，并不适用于本机应用程序，例如可视化工具中托管的托管代码。

## <a name="BKMK_Scenario"></a> 没有实时中尝试运行应用时，会显示调试程序对话框的？

请参阅 Visual Studio 中实时时应执行的操作调试程序对话框的依赖于要执行操作：

#### <a name="if-you-want-to-get-rid-of-the-dialog-box-and-just-run-the-app-normally"></a>如果你想要去掉的对话框中，而只是通常情况下运行应用

1. （高级的用户）如果已安装的 Visual Studio （或将它之前安装和已删除了它），[禁用在实时调试](#BKMK_Enabling)并尝试再次运行该应用。

2. 如果在 Internet Explorer 中运行 web 应用，禁用脚本调试。

    禁用脚本调试在 Internet 选项对话框中。 您可以访问此项从**Control Panel** / **网络和 Internet** / **Internet 选项**（的确切步骤取决于你的版本Windows 和 Internet Explorer）。

    ![JITInternetOptions](../debugger/media/jitinternetoptions.png "JITInternetOptions")

3. 重新打开在其中找到错误的网页。 如果这无法解决此问题，请联系以解决此问题的 web 应用程序所有者。

4. 如果你正在运行的 Windows 应用程序的另一种类型，需要联系应用程序的所有者，以修复此错误，并重新安装应用程序的固定的版本。

#### <a name="if-you-want-to-fix-or-debug-the-error-advanced-users"></a>如果你想要解决或调试错误 （高级用户）

- 您必须具有[安装 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/)若要查看有关错误的详细的信息，并尝试对其进行调试。 请参阅[使用 JIT](#BKMK_Using_JIT)有关的详细说明。 如果您不能解决该错误并修复应用程序，请联系应用的所有者，以解决该错误。

## <a name="BKMK_Enabling"></a> 启用或禁用在实时调试
 可以启用或禁用在实时调试 Visual Studio**工具 / 选项**对话框。

#### <a name="to-enable-or-disable-just-in-time-debugging"></a>启用或禁用实时调试

1. 打开 Visual Studio。 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在中**选项**对话框中，选择**调试**文件夹。

3. 在中**调试**文件夹，选择**中实时**页。

4. 在中**这些类型的代码启用实时调试**框中，选择或清除相关的程序类型：**托管**，**本机**，或**脚本**。

    要在启用实时调试后禁用它，必须使用管理员特权运行。 启用实时调试会设置一个注册表项，需要管理员特权才可以更改该项。

5. 单击 **“确定”** 。

   即便在你的计算机中不再安装有 Visual Studio，仍可启用实时调试。 未安装 Visual Studio 时，不能禁用中实时从 Visual Studio 调试**选项**对话框。 对于这种情况，你可以通过编辑 Windows 注册表来禁用实时调试。

#### <a name="to-disable-just-in-time-debugging-by-editing-the-registry"></a>通过编辑注册表禁用实时调试

1. 上**启动**菜单中，搜索并运行 `regedit.exe`

2. 在中**注册表编辑器**窗口中，找到并删除以下注册表项：

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger

3. 如果您的计算机正在运行 64 位操作系统，如果还要删除下列注册表项：

    - HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger

    - HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger

4. 注意不要意外删除或更改任何其他注册表项。

5. 关闭**注册表编辑器**窗口。

> [!NOTE]
> 如果想要禁用中实时调试的服务器端应用程序，这些步骤未解决该问题关闭服务器端调试在 IIS 应用程序设置，然后重试。

#### <a name="to-enable-just-in-time-debugging-of-a-windows-form"></a>为 Windows 窗体启用实时调试

1. 默认情况下，Windows 窗体应用程序有一个顶级的异常处理程序，该处理程序允许程序在能够恢复时继续运行。 例如，如果你的 Windows 窗体应用程序引发未处理的异常，将看到一个对话框，如下所示：

     ![WindowsFormsUnhandledException](../debugger/media/windowsformsunhandledexception.png "WindowsFormsUnhandledException")

     启用在实时调试的 Windows 窗体应用程序，必须执行以下附加步骤：

2. 设置`jitDebugging`值设为`true`中`system.windows.form`部分中的 machine.config 或 *\<应用程序名称 >* .exe.config 文件：

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

## <a name="a-namebkmkusingjituse-just-in-time-debugging"></a><a name="BKMK_Using_JIT">使用在实时调试
 本部分介绍可执行文件引发异常时，会发生什么情况。

 必须安装 Visual Studio，才能按照以下步骤操作。 如果未安装 Visual Studio，则可以下载免费[Visual Studio 2015 Community Edition](https://visualstudio.microsoft.com/vs/older-downloads/)。

 默认情况下，安装 Visual Studio 时会启用实时调试。

 出于本部分的目的，我们将在引发的 Visual Studio 中进行 C# 控制台应用<xref:System.NullReferenceException>。

 在 Visual Studio 中，创建一个 C# 控制台应用 (**文件 / 新建 / 项目 / Visual C# / 控制台应用程序**) 名为**ThrowsNullException**。 在 Visual Studio 中创建项目的详细信息，请参阅[演练：创建简单应用程序](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)。

 在 Visual Studio 中打开项目，打开 Program.cs 文件。 将 Main() 方法替换为以下代码，该代码会在控制台中打印一行，然后引发 NullReferenceException：

```csharp
static void Main(string[] args)
{
    Console.WriteLine("we will now throw a NullReferenceException");
    throw new NullReferenceException("this is the exception thrown by the console app");
}
```

> [!IMPORTANT]
> 为了使此过程工作[发布配置](../debugger/how-to-set-debug-and-release-configurations.md)，需要关闭[仅我的代码](../debugger/just-my-code.md)。 在 Visual Studio 中，单击**工具 / 选项**。 在中**选项**对话框中，选择**调试**。 清除该复选框，从**启用 ' 仅我的代码**。

 生成解决方案 (在 Visual Studio 中，选择**生成 / 重新生成解决方案**)。 您可以选择调试或发布配置。 有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

 生成过程将创建可执行文件 ThrowsNullException.exe。 你可以在其中创建 C# 项目的文件夹下找到它： **...\ThrowsNullException\ThrowsNullException\bin\Debug**或 **...\ThrowsNullException\ThrowsNullException\bin\Release**。

 双击 ThrowsNullException.exe。 应会看到如下的命令窗口：

 ![ThrowsNullExceptionConsole](../debugger/media/throwsnullexceptionconsole.png "ThrowsNullExceptionConsole")

 将在几秒钟后会显示一个错误窗口：

 ![ThrowsNullExceptionError](../debugger/media/throwsnullexceptionerror.png "ThrowsNullExceptionError")

 不要单击**取消**！ 将在几秒钟后，会看到两个按钮**调试**并**关闭程序**。 单击**调试**。

> [!CAUTION]
> 如果你的应用程序包含不受信任的代码，将显示一个带有一条安全警告对话框。 此对话框使可以决定是否继续调试。 在继续调试之前，请决定你是否信任相应代码。 代码是你自己编写的吗？ 你是否信任代码编写者？ 如果该应用程序正在远程计算机上运行，你是否认识进程的名称？ 即便该应用程序在本地运行，也不一定表示它是可信的应用程序。 请考虑在您的计算机上运行的恶意代码的可能性。 如果你决定，该代码您即将调试值得信任，请单击**调试**。 否则，请单击**不调试**。

 **Visual Studio 实时调试器**窗口将显示：

 ![JustInTimeDialog](../debugger/media/justintimedialog.png "JustInTimeDialog")

 下**可能的调试器**，您应该会看到**Microsoft Visual Studio 2015 的新实例**选择行。 如果已选择，请立即选择它。

 在窗口底部下**你想要使用所选的调试器进行调试？** ，单击**是**。

 ThrowsNullException 项目可打开 Visual Studio 的新实例中与引发的异常的代码行处停止执行：

 ![NullReferenceSecondInstance](../debugger/media/nullreferencesecondinstance.png "NullReferenceSecondInstance")

 可以从此时开始调试。 如果这是实际的应用程序，您需要找出原因代码抛出异常。

## <a name="just-in-time-debugging-errors"></a>实时调试错误
 如果看不到对话框中，此程序发生故障时，这可能会由于您的计算机上的 Windows 错误报告设置。 有关详细信息，请参阅[。WER 设置](https://msdn.microsoft.com/library/windows/desktop/bb513638\(v=vs.85\).aspx)。

 你可能会遇到与实时调试相关联的下列错误消息。

- **无法附加到崩溃进程。指定的程序不是 Windows 或 MS-DOS 程序。**

     当你尝试附加到以其他用户身份运行的进程时，将发生此错误。

     若要解决此问题，请启动 Visual Studio 中，打开**附加到进程**对话框从**调试**菜单中，并查找过程，你想要在调试**可用进程**列表。 如果不知道进程名称，看看**Visual Studio 实时调试器**对话框并记下进程 id。 选择中的过程**可用进程**列表中，单击**附加**。 在中**Visual Studio 实时调试器**对话框中，单击**否**以关闭对话框。

- **未能启动调试器，因为没有用户登录。**

     在没有用户登录到控制台的计算机中，如果实时调试尝试启动 Visual Studio，则会发生此错误。 因为没有用户登录，所以没有用户会话来显示“实时调试”对话框。

     要解决此问题，请登录到计算机。

- **类没有注册。**

     此错误指出：调试器尝试创建一个可能是因为安装问题而没有注册的 COM 类。

     若要解决此问题，请使用安装盘重新安装或修复 Visual Studio 安装。

## <a name="see-also"></a>请参阅
 [调试器安全](../debugger/debugger-security.md)[调试器基础知识](../debugger/debugger-basics.md)[中的实时、 调试、 选项对话框](../debugger/just-in-time-debugging-options-dialog-box.md)[安全警告：附加到不受信任的用户所拥有的进程可能很危险。如果以下信息看上去可疑或者你无法确定，请勿附加到此进程](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015)
