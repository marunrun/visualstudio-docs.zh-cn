---
title: “常规”&gt;“调试”&gt;“选项”对话框 | Microsoft Docs
ms.date: 11/09/2018
ms.topic: reference
f1_keywords:
- vs.debug.options.General
- VS.ToolsOptionsPages.Debugger.General
- VS.ToolsOptionsPages.Debugger.ENC
- vs.debug.options.ENC
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Options dialog box, debugging
ms.assetid: b33aee0b-43c3-4c26-8ed4-bc673f491503
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbd99d260ba61d9e3ae9e877ecc1cefb1a22892e
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569064"
---
# <a name="general-debugging-options"></a>常规调试选项

若要设置 Visual Studio 调试器选项，选择“工具” > “选项”，在“调试”中选中或取消选中“常规”选项旁边的选择框。 可以通过“工具”  >  “导入和导出设置” > “重置所有设置”恢复所有默认设置。 若要重置设置的子集，在做出要测试的更改之前，使用“导入和导出设置向导”保存设置，然后在以后导入保存的设置。

可以设置以下“常规”选项：

在**删除所有断点之前询问**：在完成 "**删除所有断点**" 命令前需要确认。

**在一个进程中断时中断所有进程**：当发生中断时，同时中断调试器附加到的所有进程。

**当异常跨越 AppDomain 或托管/本机边界时中断**：在托管或混合模式调试中，公共语言运行时可能会捕获跨应用程序域边界或托管/本机边界的异常，以下情况条件成立：

1. 当本机代码使用 COM 互操作调用托管代码且托管代码引发异常。 请参阅 [COM 互操作介绍](/dotnet/articles/visual-basic/programming-guide/com-interop/introduction-to-com-interop)。

2. 应用程序域 1 中运行的托管代码调用应用程序域 2 中的托管代码，且应用程序域 2 中的代码引发异常。 请参阅[应用程序域编程](/dotnet/articles/framework/app-domains/index)。

3. 代码通过使用反射调用一个函数时且该函数引发异常。 请参阅[反射](/dotnet/framework/reflection-and-codedom/reflection)。

在 2 和 3 的情况下，异常有时由 `mscorlib` 中的托管代码而非由公共语言运行时捕获。 此选项不影响在 `mscorlib` 捕获到异常时中断。

**启用地址级调试**：在地址级别启用用于调试的高级功能（"**反汇编**" 窗口、"**寄存器**" 窗口和地址断点）。

- **如果源**不可用，则显示反汇编：调试源不可用的代码时，会自动显示 "**反汇编**" 窗口。

**启用断点筛选器**：使你能够在断点上设置筛选器，使其仅影响特定的进程、线程或计算机。

**使用新的异常帮助器**：启用替换异常助手的异常帮助程序。 （从 Visual Studio 2017 开始支持 Exception Helper）

> [!NOTE]
> 对于托管代码，此选项以前称为“启用异常助手”。

**启用仅我的代码**：调试器仅显示和执行用户代码（"我的代码"），而忽略系统代码和其他经过优化或没有调试符号的代码。

- **如果启动时没有用户代码则发出警告（仅限托管）** ：调试开始时仅我的代码启用时，此选项将在没有用户代码（"我的代码"）时发出警告。

**启用 .NET Framework 源单**步执行：允许调试器单步执行 .NET Framework 源。 启用此选项会自动禁用“仅我的代码”。 .NET Framework 符号将下载到缓存位置。 使用“选项”对话框>“调试类别”>“符号”页面可更改缓存位置。

**逐过程执行属性和运算符（仅限托管）** ：阻止调试器单步执行托管代码中的属性和运算符。

**启用属性求值和其他隐式函数调用**：打开变量窗口和 "**快速监视**" 对话框中属性和隐式函数调用的自动计算。

- **对变量窗口中的对象调用字符串转换函数C# （仅限 JavaScript）** ：在变量窗口中计算对象时，执行隐式字符串转换调用。 结果显示为字符串而不是类型名称。 仅在 C# 代码中进行调试时适用。 此设置可以由 DebuggerDisplay 特性重写（请参阅[使用 DebuggerDisplay 属性](../debugger/using-the-debuggerdisplay-attribute.md)）。

**启用源服务器支持**：通知 Visual Studio 调试器从实现 srcsrv.ini （`srcsrv.dll`）协议的源服务器中获取源文件。 Team Foundation Server 和 Windows 的调试工具是实现协议的两个源服务器。 有关 Srcsrv.ini 设置的详细信息，请参阅[srcsrv.ini](/windows-hardware/drivers/debugger/srcsrv)文档。 此外，请参阅[指定符号（.pdb）和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

> [!IMPORTANT]
> 由于读取 .pdb 文件可在文件中执行任意代码，因此请确保你信任该服务器。

- 将**源服务器诊断消息打印到输出窗口**：启用源服务器支持时，此设置将启用诊断显示。

- **允许源服务器中的部分信任程序集（仅限托管）** ：启用源服务器支持时，此设置将重写不为部分信任的程序集检索源的默认行为。

- **始终运行不受信任的源服务器命令但不发出提示**：启用源服务器支持时，此设置将覆盖运行不受信任的命令时提示的默认行为。

**启用源链接支持**：通知 Visual Studio 调试器下载包含源链接信息的 *.pdb*文件的源文件。 有关源链接的详细信息，请参阅[源链接规范](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/source_link.md)。

> [!IMPORTANT]
> 由于源链接将使用 http 或 https 下载文件，因此请确保你信任该 .pdb 文件。

- **回退到所有源链接请求的 Git 凭据管理器身份验证**：启用源链接支持后，源链接请求将无法通过身份验证，Visual Studio 会调用 Git 凭据管理器。

**为断点和当前语句突出显示整行C++ （仅）** ：调试器突出显示断点或当前语句时，它将突出显示整行。

**要求源文件与原始版本完全匹配**：通知调试器验证源文件是否与用于生成正在调试的可执行文件的源代码版本相匹配。 若版本不匹配，系统会提示你查找匹配的源。 若找不到匹配的源，调试过程中将不会显示源代码。

将**所有输出窗口文本重定向到即时窗口**：将通常显示在 "**输出**" 窗口中的所有调试器消息改为发送到 "**即时**" 窗口。

**在变量窗口中显示对象的原始结构**：关闭所有对象结构视图自定义。 有关视图自定义的详细信息，请参阅[创建托管对象的自定义视图](../debugger/create-custom-views-of-managed-objects.md)。

**在模块加载时取消 jit 优化（仅限托管）** ：在加载模块时禁用托管代码的 jit 优化，并在附加调试器时编译 jit。 禁用优化可能更易于调试某些问题，尽管这会降低性能。 如果正在使用“仅我的代码”，则取消 JIT 优化会导致非用户代码显示为用户代码（“我的代码”）。 有关详细信息，请参阅[JIT 优化和调试](../debugger/jit-optimization-and-debugging.md)。

**为 ASP.NET （Chrome、Microsoft Edge 和 IE）启用 JavaScript 调试**：为 ASP.NET 应用启用脚本调试器。 第一次在 Chrome 中使用时，可能需要登录到浏览器来启用已安装的 Chrome 扩展。 禁用此选项以恢复到旧行为。

**启用 Uwp Javascript 应用的边缘开发人员工具（实验）** ：在 Microsoft Edge 中启用适用于 uwp javascript 应用的开发人员工具。

**启用旧版 Chrome javascript 调试器 for ASP.NET**：对 ASP.NET 应用启用旧版 chrome javascript 脚本调试器。 第一次在 Chrome 中使用时，可能需要登录到浏览器来启用已安装的 Chrome 扩展。

**当以管理员身份运行 Visual studio 时，使用实验性方式启动 Chrome JavaScript 调试**：告诉 Visual Studio 在 JavaScript 调试期间尝试一种新的启动 chrome 的方式。

**加载 dll 导出（仅限本机）** ：加载 dll 导出表。 处理 Windows 消息、Windows 过程 (WindowProc)、COM 对象、封送或不具有其符号的任何 DLL 时，DLL 导出表中的符号信息将很有用。 读取 DLL 导出信息会占用一些系统开销。 因此，默认情况下此功能被禁用。

若要查看 DLL 导出表中的可用符号，请使用 `dumpbin /exports`。 符号可用于任何 32 位系统 DLL。 从 `dumpbin /exports` 输出中，可以查看到精确的函数名，包括非字母数字字符。 这对于在函数上设置断点很有用。 DLL 导出表中的函数名在调试器的其他位置似乎被截断了。 调用将按调用顺序列出，当前函数（嵌套最深的函数）位于顶端。 有关详细信息，请参阅 [dumpbin /exports](/cpp/build/reference/dash-exports)。

**向下显示并行堆栈关系图**：控制在 "**并行堆栈**" 窗口中显示堆栈的方向。

**如果写入的数据未更改值，则忽略 GPU 内存访问异常**：如果数据未更改，则忽略在调试期间检测到的争用情况。 有关详细信息，请参阅[调试 GPU 代码](../debugger/debugging-gpu-code.md)。

**使用托管兼容模式**：将默认调试引擎替换为旧版本，以启用以下方案：

- 你使用的不是C#、Visual Basic 的 .net 语言，或者F#提供自己的表达式计算器的 .net 语言（ C++这包括/cli）。

- 想要在混合模式调试过程中为 C++ 项目启用“编辑并继续”。

> [!NOTE]
> 选择托管兼容模式会禁用仅在默认调试引擎中实现的某些功能。 旧版调试引擎已替换为 Visual Studio 2012。

**使用旧版C#和 VB 表达式计算器**：调试器将使用 Visual Studio 2013 C#或 Visual Basic 表达式计算器，而不是基于 Visual Studio 2015 Roslyn 的表达式计算器。

**对潜在的不安全进程使用自定义调试器可视化工具时发出警告（仅限托管）** ：当使用在调试的进程中运行代码的自定义调试器可视化工具时，Visual Studio 将发出警告，因为它可能正在运行不安全代码.

**启用 windows 调试堆分配器（仅限本机）** ：允许 Windows 调试堆改进堆诊断。 启用此选项会影响调试性能。

**启用 XAML 的 UI 调试工具**：启动调试（**F5**）受支持的项目类型时，将显示 "实时可视化树" 和 "实时属性浏览" 窗口。 有关详细信息，请参阅[调试时检查 XAML 属性](../xaml-tools/inspect-xaml-properties-while-debugging.md)。

- **预览实时可视化树中的所选元素**：在 "**实时可视化树**" 窗口中选择了其上下文的 XAML 元素。

- **在应用程序中显示运行时工具**：在要调试的 XAML 应用程序的主窗口上的工具栏中显示**实时可视化树**命令。 Visual Studio 2015 Update 2 中引入了此选项。

- **启用 Xaml 热重载**：使你能够在应用程序运行时将 Xaml 热重载功能与 xaml 代码一起使用。 （此功能之前称为 "XAML 编辑并继续"）

**调试时启用诊断工具**：调试时，将显示 "**诊断工具**" 窗口。

**显示调试时的运行时间 perftips**：代码窗口显示调试时给定方法调用的运行时间。

**启用 "编辑并继续**"：在调试时启用 "编辑并继续" 功能。

- **启用本机 "编辑并继续**"：在调试本机C++代码时，可以使用 "编辑并继续" 功能。 有关详细信息，请参阅[编辑并继续C++（）](../debugger/edit-and-continue-visual-cpp.md)。

- **在继续时应用更改（仅限本机）** ： Visual Studio 会自动编译和应用在从中断状态继续进程时所做的任何未处理的代码更改。 可选择使用“调试”菜单下的“应用代码更改”项来应用更改（如果尚未选择）。

- **针对陈旧代码发出警告（仅限本机）** ：获取有关陈旧代码的警告。

**调试时显示运行以在编辑器中单击按钮**：选择此选项时，将在调试时显示 "[运行到单击](../debugger/debugger-feature-tour.md#run-to-a-point-in-your-code-quickly-using-the-mouse)" 按钮。

**调试停止时自动关闭控制台**：通知 Visual Studio 在调试会话结束时关闭控制台。

::: moniker range=">= vs-2019"
**启用快速表达式计算（仅限托管）** ：允许调试器通过模拟简单属性和方法的执行来尝试更快速地进行评估。
::: moniker-end

## <a name="options-available-in-older-versions-of-visual-studio"></a>早期版本的 Visual Studio 中可用的选项

如果你使用的是较旧版本的 Visual Studio，则可能会出现一些其他选项。

**启用异常助手**：对于托管代码，启用异常助手。 从 Visual Studio 2017 开始，异常帮助程序替换了异常助手。

**在未经处理的异常上展开调用堆栈**：导致 "**调用堆栈**" 窗口将调用堆栈回滚到未经处理的异常发生之前的点。

**如果启动时没有符号，则发出警告（仅限本机）** ：在调试调试器没有符号信息的程序时，将显示警告对话框。

**如果启动时禁用了脚本调试，则发出**警告：当启动调试器时禁用了脚本调试，将显示警告对话框。

**使用本机兼容模式**：选择此选项时，调试器将使用 Visual Studio 2010 本机调试器而不是新的本机调试器。

- 如果正在调试 .NET C++ 代码，请使用此选项，因为新的调试引擎不支持计算 .NET C++ 表达式。 但是，启用本机兼容模式会禁用依赖于当前调试器实现来操作的许多功能。 例如，旧引擎缺少许多用于内置类型（如 Visual Studio 2015 项目中的 `std::string`）的可视化工具。   为获得最佳调试体验，在这些应用场景中请使用 Visual Studio 2013 项目。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
