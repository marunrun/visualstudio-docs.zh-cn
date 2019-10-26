---
title: 使用实时调试器进行调试 |Microsoft Docs
ms.date: 09/24/2018
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 32a3ebd6e9047271a21425ac5b7eaaf715955b61
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911394"
---
# <a name="debug-using-the-just-in-time-debugger-in-visual-studio"></a>在 Visual Studio 中使用实时调试器进行调试

当一个在 Visual Studio 之外运行的应用发生错误或崩溃时，实时调试可自动启动 Visual Studio。 使用实时调试，可以测试 Visual Studio 外部的应用，并可在出现问题时打开 Visual Studio 开始调试。

实时调试适用于 Windows 桌面应用。 它不适用于通用 Windows 应用，也不适用于托管在本机应用程序（如可视化器）中的托管代码。

> [!TIP]
> 如果只想让实时调试器对话框停止显示，而不安装 Visual Studio，请参阅[禁用实时调试器](../debugger/just-in-time-debugging-in-visual-studio.md)。 如果已安装 Visual Studio，可能需要[从 Windows 注册表禁用实时调试](#disable-just-in-time-debugging-from-the-windows-registry)。

## <a name="BKMK_Enabling"></a> 在 Visual Studio 中启用或禁用实时调试

>[!NOTE]
>若要启用或禁用实时调试，必须以管理员身份运行 Visual Studio。 启用或禁用实时调试会设置一个注册表项，可能需要管理员权限来更改此注册表项。 若要以管理员身份打开 Visual Studio，右键单击 Visual Studio 应用程序，然后选择**以管理员身份运行**。

可从 Visual Studio 的“工具” > “选项”（或“调试” > “选项”）对话框中配置实时调试。

**启用或禁用实时调试：**

1. 在“工具”或“调试”菜单上，选择“选项” > “调试” > “实时”。

   ![启用或禁用 JIT 调试](../debugger/media/dbg-jit-enable-or-disable.png "启用或禁用 JIT 调试")

1. 在“为这些类型的代码启用实时调试”框中，选择希望通过实时调试进行调试的代码类型：“托管”、“本机”和/或“脚本”。

1. 选择“确定”。

如果启用了实时调试器，但它并未在应用程序崩溃或出错时打开，请参阅[实时调试疑难解答](#jit_errors)。

## <a name="disable-just-in-time-debugging-from-the-windows-registry"></a>从 Windows 注册表禁用实时调试

即便计算机中不再安装有 Visual Studio，仍可启用实时调试。 如果不再安装 Visual Studio，则可以通过编辑 Windows 注册表来禁用实时调试。

**若要通过编辑注册表禁用实时调试，请执行以下操作：**

1. 从 Windows“开始”菜单，运行“注册表编辑器”(regedit.exe)。

2. 在 "**注册表编辑器**" 窗口中，找到并删除以下注册表项：

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    ![JIT 注册表项](../debugger/media/dbg-jit-registry.png "JIT 注册表项")

3. 如果计算机运行的是64位操作系统，还请删除以下注册表项：

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    请确保不要删除或更改任何其他注册表项。

5. 关闭 "**注册表编辑器**" 窗口。

## <a name="enable-just-in-time-debugging-of-a-windows-form"></a>启用 Windows 窗体的实时调试

默认情况下，Windows 窗体应用具有一个顶级异常处理程序，可让应用保持运行（如果能够恢复）。 如果 Windows 窗体应用引发未处理的异常，则会显示以下对话框：

![Windows 窗体未经处理的异常](../debugger/media/windowsformsunhandledexception.png "Windows 窗体未经处理的异常")

若要启用实时调试而不是标准 Windows 窗体错误处理，请添加以下设置：

- 在 machine.config 或 \<应用名称>.exe.config 文件的 `system.windows.forms` 部分中，将 `jitDebugging` 值设置为 `true`****:

    ```xml
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```

- 在 C++ 窗体应用程序中，还要在 *.config* 文件或代码中将 `DebuggableAttribute` 设置为 `true`。 如果使用 [/Zi](/cpp/build/reference/z7-zi-zi-debug-information-format) 而不使用 [/Og](/cpp/build/reference/og-global-optimizations) 进行编译，则编译器会替你设置此属性。 但是，如果要调试非优化发布版本，则必须通过在应用的 AssemblyInfo.cpp 文件中添加以下行来设置 `DebuggableAttribute`：

   ```cpp
   [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
   ```

   有关更多信息，请参见<xref:System.Diagnostics.DebuggableAttribute>。

## <a name="BKMK_Using_JIT"></a>使用实时调试
此示例演示在应用引发错误时如何进行实时调试。

- 必须安装 Visual Studio，才能按照以下步骤操作。 如果未安装 Visual Studio，则可以免费下载 [Visual Studio Community Edition](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)。

- 请务必依次选择“工具” > “选项” > “调试” > “实时”，[启用](#BKMK_Enabling)实时调试。

本示例会在 Visual Studio 中创建 C# 控制台应用，该应用可引发 [NullReferenceException](/dotnet/api/system.nullreferenceexception)。

1. 在 visual Studio 中，创建C#名为*ThrowsNullException*的控制台应用（**文件** > **新建** > **项目** > **Visual C#**  > **控制台应用程序**）。 有关在 Visual Studio 中创建项目的详细信息，请参阅[演练：创建简单的应用程序](/visualstudio/get-started/csharp/tutorial-wpf)。

1. 在 Visual Studio 中打开项目时，请打开 *Program.cs* 文件。 将 Main() 方法替换为以下代码，该代码会在控制台中打印一行，然后引发 NullReferenceException：

   ```csharp
   static void Main(string[] args)
   {
       Console.WriteLine("we will now throw a NullReferenceException");
       throw new NullReferenceException("this is the exception thrown by the console app");
   }
   ```

1. 若要生成解决方案，请选择“调试”（默认值） 或“发布”配置，然后选择“生成” > “重新生成解决方案”.

   > [!NOTE]
   > - 选择 "**调试**配置" 以获取完整的调试体验。
   > - 如果选择[发布](../debugger/how-to-set-debug-and-release-configurations.md)配置，必须先关闭[仅我的代码](../debugger/just-my-code.md)才能运行此过程。 可在“工具” > “选项” > “调试”下，取消选择“启用仅我的代码”。

   有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

1. 在 C# 项目文件夹 ( *...\ThrowsNullException\ThrowsNullException\bin\Debug*或 *...\ThrowsNullException\ThrowsNullException\bin\Release*) 中打开生成的应用 *ThrowsNullException.exe*。

   应会看到以下命令窗口：

   ![ThrowsNullExceptionConsole](../debugger/media/throwsnullexceptionconsole.png "ThrowsNullExceptionConsole")

1. 此时将打开 "**选择实时调试器**" 对话框。

   ![JustInTimeDialog](../debugger/media/justintimedialog.png "JustInTimeDialog")

   在“可用调试器”下，选择“\<首选 Visual Studio 版本>的新实例”（如果尚未选择）。

1. 选择“确定”。

   ThrowsNullException 项目会在 Visual Studio 的新实例中打开，并在引发异常的代码行处停止执行：

   ![NullReferenceSecondInstance](../debugger/media/nullreferencesecondinstance.png "NullReferenceSecondInstance")

可以从此时开始调试。 如果调试的是真实应用，则需要找出代码引发异常的原因。

> [!CAUTION]
> 如果应用包含不受信任的代码，则会出现安全警告对话框，让你可决定是否继续进行调试。 继续调试前，请确定是否信任该代码。 代码是否为自己编写的？ 如果应用程序在远程计算机上运行，你能否识别进程的名称？ 如果应用在本地运行，请考虑计算机上运行恶意代码的可能性。 如果决定信任该代码，请选择“确定”。 否则，请选择“取消”。

## <a name="jit_errors"></a>实时调试疑难解答

如果在应用崩溃时实时调试不启动，即使 Visual Studio 中已启用实时调试也是如此，则：

- Windows 错误报告可能会接管计算机上的错误处理。

  若要解决此问题，请使用注册表编辑器将**值**为**1**的**已禁用**的**DWORD 值**添加到以下注册表项：

  - **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows 错误报告**

  - （适用于64位计算机）： **HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows\Windows 错误报告**

  有关详细信息，请参阅 [.WER 设置](/windows/desktop/wer/wer-settings)。

- 已知的 Windows 问题可能导致实时调试器启动失败。

  解决方法是将值为**1**的**自动** **值**的**DWORD 值**添加到以下注册表项：

  - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug**

  - （适用于64位计算机）： **HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug**

在实时调试过程中，你可能会看到以下错误消息：

- **无法附加到崩溃进程。指定的程序不是 Windows 或 MS-DOS 程序。**

    调试器尝试附加到在另一个用户下运行的进程。

    若要解决此问题，请在 Visual Studio 中依次打开“调试” > “附加到进程”，然后在“可用进程”列表中查找要调试的进程。 如果不清楚进程名称，请在“Visual Studio 实时调试器”对话框中查找进程 ID。 在“可用进程”列表中选择该进程，然后选择“附加”。 选择“否”可关闭“实时调试器”对话框。

- **未能启动调试器，因为没有用户登录。**

    没有用户登录到控制台，因此没有用户会话来显示实时调试对话框。

    要解决此问题，请登录到计算机。

- **类没有注册。**

    调试器试图创建的 COM 类未进行注册，可能是由安装问题导致。

    若要解决此问题，请使用 Visual Studio 安装程序重新安装或修复 Visual Studio 安装。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [初探调试器](../debugger/debugger-feature-tour.md)
- ["选项"、"调试"、"实时" 对话框](../debugger/just-in-time-debugging-options-dialog-box.md)
- [安全警告附加到不受信任的用户所拥有的进程可能很危险。如果以下信息看上去可疑或者你无法确定，请勿附加到此进程](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
