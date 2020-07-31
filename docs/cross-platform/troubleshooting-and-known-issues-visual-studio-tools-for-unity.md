---
title: 疑难解答和已知问题 (VS Tools for Unity)
ms.custom: ''
ms.date: 07/03/2018
ms.technology: vs-unity-tools
ms.topic: troubleshooting
ms.assetid: 8f5db192-8d78-4627-bd07-dbbc803ac554
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 41ef89bbb7b3595c24de5a482eed805e75eb2cdb
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87235077"
---
# <a name="troubleshooting-and-known-issues-visual-studio-tools-for-unity"></a>疑难解答和已知问题 (Visual Studio Tools for Unity)

本部分将介绍 Visual Studio Tools for Unity 常见问题的解决方案、已知问题的说明并了解如何通过报告错误来帮助改进 Visual Studio Tools for Unity。

## <a name="troubleshooting-the-connection-between-unity-and-visual-studio"></a>Unity 和 Visual Studio 之间的连接疑难解答

### <a name="confirm-editor-attaching-is-enabled"></a>确认已启用“编辑器连接”

在 Unity 菜单中，选择“编辑”>“首选项”，然后选择“外部工具”选项卡 。确定已启用“编辑器连接”复选框。 有关详细信息，请查阅 [Unity 首选项文档](https://docs.unity3d.com/Manual/Preferences.html)。

### <a name="unable-to-attach"></a>无法附加

- 尝试暂时禁用防病毒软件，或同时为 VS 和 Unity 创建排除规则。
- 尝试暂时禁用防火墙，或创建规则，允许在 VS 和 Unity 之间建立 TCP/UDP 网络。
- Team Viewer 之类的某些程序可能会干扰进程检测。 可以尝试暂停任何外部软件，看看它是否更改了某些内容。
- 请勿重命名主要 Unity 可执行文件，因为 VSTU 只监视“Unity.exe”进程。

## <a name="visual-studio-crashes"></a>Visual Studio 崩溃

此问题可能是由 Visual Studio MEF 缓存损坏导致的。

尝试删除以下文件夹以重置 MEF 缓存（执行此操作之前请关闭 Visual Studio）：

```batch
%localappdata%\Microsoft\VisualStudio\<version>\ComponentModelCache
```

这样应该能够解决问题。 如果仍然有问题，请以管理员身份运行 Visual Studio 的开发人员命令提示，并使用以下命令：

```batch
 devenv /setup
```

## <a name="visual-studio-stops-responding"></a>Visual Studio 停止响应

Parse、FMOD、UMP (Universal Media Player)、ZFBrowser 或嵌入式浏览器等几个 Unity 插件使用本机线程。 插件在最后将本机线程附加到运行时，阻止了对操作系统的调用，这时就会出现问题。 这意味着 Unity 不能对调试程序（或域重载）中断该线程并停止响应。

有一种解决方法适合 FMOD：通过传递 `FMOD_STUDIO_INIT_SYNCHRONOUS_UPDATE` 初始化[标记](https://www.fmod.com/resources/documentation-studio?version=2.0&page=https://fmod.com/resources/documentation-api?version=2.0&page=studio-api-system.html#fmod_studio_initflags)来禁用异步处理，并对主线程执行所有处理。

## <a name="incompatible-project-in-visual-studio"></a>Visual Studio 中的不兼容项目

首先，检查是否已将 Visual Studio 设置为 Unity 中的外部脚本编辑器（编辑/首选项/外部工具）。 然后检查 Unity 是否已安装 Visual Studio 插件（“帮助/关于”必须在底部显示一条类似于“已启用 Microsoft Visual Studio Tools for Unity”的消息）。 然后检查 Visual Studio 中是否已正确安装该扩展（“帮助/关于”）。

## <a name="extra-reloads-or-visual-studio-losing-all-open-windows"></a>其他重载，或 Visual Studio丢失所有打开的窗口

请勿直接从资产处理器或任何其他工具接触项目文件。 如果确实需要对项目文件进行操作，我们为此公开了 API。 请检查[程序集引用问题部分](#assembly-reference-issues)。

如果遇到其他重载或 Visual Studio 在重载时丢失所有打开的窗口，请确保安装有合适的 .NET 目标包。 查看以下部分，了解有关框架的详细信息。

## <a name="the-debugger-does-not-break-on-exceptions"></a>调试程序不会异常中断

使用旧版 Unity 运行时（.NET 3.5 等效版本）情况下，未处理异常时（在 try/catch 块外部），调试程序将始终中断。 如果已处理了异常，则调试程序将使用异常设置窗口来确定是否需要中断。

借助新的运行时（.NET 4.6 等效版本），Unity 引入了一种管理用户异常的新方法，因此即使所有异常都在 try/catch 块外部，也会将这些异常视为“用户已处理”。 这就是希望调试程序中断时，需要在“异常设置”窗口显式检查它们的原因。

在 “异常设置”窗口（“调试”>“窗口”>“异常设置”）中，展开某个类别异常的节点（例如，表示 .NET 异常的公共语言运行时异常），并选中想要在该类别中捕获的特定异常的复选框（例如，System.NullReferenceException）。 还可以选择整个类别的异常。

## <a name="on-windows-visual-studio-asks-to-download-the-unity-target-framework"></a>在 Windows 上，Visual Studio 会要求下载 Unity 目标框架

Visual Studio Tools for Unity 要求安装 .NET framework 3.5（默认情况下在 Windows 8 或 10 上未安装）。 若要解决此问题，请按照说明下载并安装 .NET framework 3.5。

使用新的 Unity 运行时还需要 .NET 目标包版本 4.6 和 4.7.1。 可以使用 VS2017 安装程序快速安装它们（修改 VS2017 安装、单个组件、.NET 类别，并选择所有 4.x 目标包）。

## <a name="assembly-reference-issues"></a>程序集引用问题

如果项目中存在复杂引用，或者如果希望能更好地控制此生成步骤，可以使用我们的 [API](../cross-platform/customize-project-files-created-by-vstu.md) 来操作生成的项目或解决方案内容。 也可以在 Unity 项目中使用[响应文件](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html)，我们将对它们进行处理。

## <a name="breakpoints-with-a-warning"></a>带有警告的断点

如果 Visual Studio 无法找到特定断点的源位置，系统会在断点附近显示一条警告消息。 检查当前的 Unity 场景中是否已正确加载/使用你正在使用的脚本。

## <a name="breakpoints-not-hit"></a>未命中断点

检查当前的 Unity 场景中是否已正确加载/使用你正在使用的脚本。 退出 Visual Studio 和 Unity，然后删除生成的所有文件（\*.csproj、\*.sln）和整个库文件夹。

## <a name="unable-to-debug-android-players"></a>无法调试 Android 播放器

我们使用多播进行播放器检测（这是 Unity 使用的默认机制），但之后我们会使用常规 TCP 连接来附加调试器。 检测阶段是 Android 设备的主要问题。

Wifi 是通用的，但与 USB 比起来非常慢，因为存在延迟。 我们已经了解，某些路由器或设备缺少正确多播支持（众所周知，Nexus 系列就存在这个问题）。

USB 调试速度非常快，Visual Studio Tools for Unity 现可检测 USB 设备，并与 adb 服务器对话，使其正确转接接口以进行调试。

## <a name="issues-with-visual-studio-2015-and-intellisense-or-code-coloration"></a>Visual Studio 2015 和 IntelliSense 或代码着色出现问题

请尝试将 Visual Studio 2015 升级到 update 3。

## <a name="known-issues"></a>已知问题

 在 Visual Studio Tools for Unity 中存在一些已知问题，是由调试器与 Unity 的旧版本的 C# 编译器的交互方式导致的。 我们正设法帮助解决这些问题，但在此期间，你可能会遇到以下问题：

- 在调试时，Unity 有时会崩溃。

- 在调试时，Unity 有时会冻结。

- 有时单步执行和跳出方法的方式不正确，尤其是在迭代器中或在 switch 语句内。

## <a name="report-errors"></a>报告错误

 请在遇到崩溃、冻结或其他错误时发送错误报告以帮助我们改进 Visual Studio Tools for Unity 的质量。 这可以帮助我们调查并修复 Visual Studio Tools for Unity 中的问题。 谢谢！

### <a name="how-to-report-an-error-when-visual-studio-freezes"></a>如何在 Visual Studio 冻结时报告错误

 有报告表明使用 Visual Studio Tools for Unity 进行调试时 Visual Studio 有时会冻结，但我们需要更多的数据来了解这个问题。 你可以通过执行下面的步骤来帮助我们调查。

##### <a name="to-report-that-visual-studio-freezes-while-debugging-with-visual-studio-tools-for-unity"></a>报告使用 Visual Studio Tools for Unity 进行调试时 Visual Studio 会冻结

在 Windows 上：

1. 打开 Visual Studio 的新实例。

1. 打开“附加到进程”对话框。 在 Visual Studio 的新实例中的主菜单上，选择“调试” 、“附加到进程” 。

1. 将调试器附加到 Visual Studio 的已冻结的实例。 在“附加到进程”  对话框中，从“可用进程”  表中选择 Visual Studio 的已冻结实例，然后选择“附加”  按钮。

1. 暂停调试器。 在 Visual Studio 的新实例中的主菜单上，依次选择“调试”、“全部中断”或只需按 Ctrl + Alt + Break 即可  。

1. 创建线程转储。 在命令窗口中，输入以下命令并按 Enter：

    ```powershell
    Debug.ListCallStack /AllThreads /ShowExternalCode
    ```

    你可能首先需要使“命令”  窗口可见。 在 Visual Studio 中的主菜单上，选择“视图” 、“其他窗口” 、“命令窗口” 。

在 Mac 上：

1. 打开终端并获取 Visual Studio for Mac 的 PID：

    ```shell
    ps aux | grep "[V]isual Studio.app"
    ```

1. 启动 lldb 调试程序：

    ```shell
    lldb
    ```

1. 使用 PID 附加到 Visual Studio for Mac 实例：

    ```shell
    process attach --pid THE_PID_OF_THE_VSFM_PROCESS
    ```

1. 检索所有线程的 stacktrace：

    ```shell
    bt all
    ```

最后，将线程转储以及 Visual Studio 冻结时你正在执行的操作的说明一起发送到 [vstusp@microsoft.com](mailto:vstusp@microsoft.com)。

## <a name="see-also"></a>请参阅

- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
