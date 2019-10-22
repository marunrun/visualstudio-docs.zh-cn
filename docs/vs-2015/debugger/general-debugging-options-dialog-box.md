---
title: “常规”&gt;“调试”&gt;“选项”对话框 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.options.General
- VS.ToolsOptionsPages.Debugger.General
- VS.ToolsOptionsPages.Debugger.ENC
- vs.debug.options.ENC
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- Options dialog box, debugging
ms.assetid: b33aee0b-43c3-4c26-8ed4-bc673f491503
caps.latest.revision: 50
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6c53af4a8e0f42708ab94d7206a9c0cc54819798
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573541"
---
# <a name="general-debugging-options-dialog-box"></a>“选项”对话框 ->“调试”->“常规”
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过 "**工具"/"选项"/"调试"/"常规**" 页可以设置以下选项：  
  
 **删除所有断点之前询问**  
 在完成“删除所有断点”命令前需要进行确认。  
  
 **在一个进程中断时中断所有进程**  
 发生一个中断时，同时中断调试器连接到的所有进程。  
  
 **当异常跨越 AppDomain 或托管/本机边界时中断**  
 在托管或混合模式调试中，如果满足以下条件，公共语言运行时可能会捕获跨越应用程序域边界或托管/本机边界的异常：  
  
 1 \) 当本机代码使用 COM 互操作调用托管代码而托管代码引发异常时。 请参阅 [COM 互操作介绍](https://msdn.microsoft.com/library/8bd62e68-383d-407f-998b-29aa0ce0fd67)。  
  
 2 \) 当应用程序域1中运行的托管代码调用应用程序域2中的托管代码时，应用程序域2中的代码将引发异常。 请参阅[应用程序域编程](https://msdn.microsoft.com/bd36055b-56bd-43eb-b4d8-820c37172131)。  
  
 3 \) 当代码使用反射调用函数时，该函数将引发异常。 请参阅[反射](https://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775)。  
  
 在第 2) 和 3) 条中，异常有时由 `mscorlib` 中的托管代码而不是公共语言运行时捕获。 此选项不影响在 `mscorlib` 捕获到异常时中断。  
  
 **启用地址级调试**  
 启用高级功能在地址级上进行调试（“反汇编”窗口、“注册”窗口和地址断点)。  
  
 **如果源不可用，则显示反汇编**  
 当你尝试调试源不可用的代码时，会自动显示 "**反汇编**" 窗口。  
  
 **启用断点筛选器**  
 使您能够对断点设置筛选器，使其仅影响特定的进程、线程或计算机。  
  
 **启用异常助手**  
 仅用于托管代码。 托管异常打开“异常助手”对话框。  请参阅[异常助手](https://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb)。  
  
 **在未经处理的异常上展开调用堆栈**  
 导致“调用堆栈”窗口将调用堆栈回滚到未经处理的异常发生之前的时间点。  
  
 **启用“仅我的代码”**  
 调试器仅显示和单步执行用户代码（“我的代码”），而忽略系统代码和其他经过优化或没有调试符号的代码。  
  
 **在变量窗口中显示非用户对象的所有成员（仅 Visual Basic）**  
 启用非用户代码（不是“我的代码”）中对象内的非公共成员的显示。  
  
 **如果启动时没有用户代码，则发出警告**  
 如果在调试时启用“仅我的代码”，此选项会在没有用户代码（“我的代码”）的情况下发出警告。  
  
 **启用 .NET Framework 源单步执行**  
 允许调试器单步执行 .NET Framework 源代码。 自动启用此选项会禁用“仅我的代码”，.NET Framework 符号将下载到缓存位置。 可以在 "**选项**" 对话框的 "**调试**" 类别，"**符号**" 页中更改缓存位置。  
  
 **逐过程执行属性和运算符（仅限托管）**  
 防止调试器单步执行托管代码中的属性和运算符。  
  
 **启用属性求值和其他隐式函数调用**  
 在变量窗口和“快速监视”对话框中打开属性的自动求值和隐式函数调用。  
  
 **对变量窗口中的对象调用字符串转换函数C# （仅限 JavaScript）**  
 在变量窗口中计算对象时，执行隐式字符串转换调用。 因此，结果将显示为字符串而不是类型名。 仅在 C# 代码中进行调试时适用。 此设置可以由 DebuggerDisplay 特性重写（请参阅[使用 DebuggerDisplay 属性](../debugger/using-the-debuggerdisplay-attribute.md)）。  
  
 **启用源服务器支持**  
 指示 Visual Studio 调试器从实现 SrcSrv (`srcsrv.dll`) 协议的源服务器中获取源文件。 Team Foundation Server 和 Windows 的调试工具是实现协议的两个源服务器。 有关 SrcSrv 设置的更多信息，请参阅“Windows 的调试工具”文档。 此外，请参阅[指定符号（.pdb）和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。  
  
> [!IMPORTANT]
> 由于读取 .pdb 文件会执行文件中的任意代码，因此请确保你信任此服务器。  
  
 **将源服务器诊断消息打印到输出窗口**  
 如果启用源服务器支持，此设置会打开诊断显示。  
  
 **允许源服务器中的部分信任程序集（仅限托管）**  
 若源服务器支持已启用，此设置将替代不检索部分信任程序集的源这一默认行为。  
  
 **为断点和当前语句突出显示整行**  
 调试器突出显示断点或当前语句时，会突出显示整个行。  
  
 **要求源文件与原始版本完全匹配**  
 指示调试器验证源文件是否与用于构建待调试的可执行文件的源代码版本匹配。 如果版本不匹配，则会提示你查找匹配源。 若找不到匹配的源，调试过程中将不会显示源代码。  
  
 **将所有输出窗口文本重定向到即时窗口**  
 将通常显示在“输出”窗口中的所有调试器消息发送到“即时”窗口。  
  
 **在变量窗口中显示对象的原始结构**  
 禁用所有对象的结构视图自定义。 有关视图自定义的详细信息，请参阅[创建托管对象的自定义视图](../debugger/create-custom-views-of-managed-objects.md)。  
  
 **在模块加载时取消 JIT 优化（仅限托管）**  
 在附加调试器的情况下，加载模块并编译 JIT 后，禁用托管代码的 JIT 优化。 禁用优化可能更易于调试某些问题，尽管这会降低性能。 如果正在使用“仅我的代码”，则取消 JIT 优化会导致非用户代码显示为用户代码（“我的代码”）。  
  
 **如果启动时没有任何符号则发出警告（仅限本机）**  
 如果尝试调试在调试器中没有对应符号信息的程序，则会显示警告对话框。  
  
 **如果启动时禁用了脚本调试，则发出警告**  
 如果在启动调试器时禁用了脚本调试，则会显示警告对话框。  
  
 **加载 dll 导出**  
 加载 DLL 导出表。 处理 Windows 消息、Windows 过程 (WindowProc)、COM 对象、封送或不具有其符号的任何 DLL 时，DLL 导出表中的符号信息将很有用。 读取 DLL 导出信息会占用一些系统开销。 因此，默认情况下此功能被禁用。  
  
 若要查看 DLL 导出表中的可用符号，请使用 `dumpbin /exports`。 符号可用于任何 32 位系统 DLL。 从 `dumpbin /exports` 输出中，可以查看到精确的函数名，包括非字母数字字符。 这对于在函数上设置断点很有用。 DLL 导出表中的函数名在调试器的其他位置似乎被截断了。 调用将按调用顺序列出，当前函数（嵌套最深的函数）位于顶端。 有关详细信息，请参阅[dump bin/exports](https://msdn.microsoft.com/library/2971ab7e-4ee6-478b-9c85-cda42a4ce1bf)。  
  
 **自下而上显示并行堆栈关系图**  
 控制堆栈在“并行堆栈”窗口中的显示方向。  
  
 **如果写入的数据未更改值，则忽略 GPU 内存访问异常**  
 如果数据未改变，则忽略在调试期间检测的争用条件。 有关详细信息，请参阅[调试 GPU 代码](../debugger/debugging-gpu-code.md)。  
  
 **使用托管兼容模式**  
 将默认调试引擎替换为旧版本，以支持以下方案：  
  
- 使用除 C#、VB 或 F# 之外，拥有自己的表达式计算器（包括 C++/CLI）的其他 .NET Framework 语言。  
  
- 在执行混合模式调试时，你想要为 C++ 项目启用“编辑并继续”。  
  
  注意，选择托管兼容模式会禁用仅可在默认调试引擎中实现的一些功能。  
  
  **使用本机兼容模式**  
  选中此选项后，调试器使用 Visual Studio 2010 本机调试器而不是新的本机调试器。  
  
  因为新的调试引擎不支持计算 .NET C++ 表达式，因此应在调试 .NET C++ 代码时使用此选项。 但是，启用本机兼容模式会禁用依赖于当前调试器实现来操作的许多功能。 例如，旧引擎缺少许多用于内置类型（如 Visual Studio 2015 项目中的 `std::string`）的可视化工具。  为获得最佳调试体验，在这些应用场景中请使用 Visual Studio 2013 项目。  
  
  **使用旧版C#和 VB 表达式计算器**  
  调试器将使用 Visual Studio 2013 C# /VB 表达式计算器，而不是基于 Visual Studio 2015 Roslyn 的表达式计算器。  
  
  **对潜在的不安全进程使用自定义调试器可视化工具时发出警告（仅限托管）**  
  当你使用在调试对象进程中运行代码的自定义调试器可视化工具时，Visual Studio 会对你发出警告，因为它可能在运行不安全代码。  
  
  **启用 Windows 调试堆分配器（仅限本机）**  
  启用 Windows 调试堆以改进堆诊断。 启用此选项会影响调试性能。  
  
  **启用 XAML 的 UI 调试工具**  
  在开始调试 (F5) 支持的项目类型时，将显示“实时可视化树”和“实时属性资源管理器”窗口。 有关详细信息，请参阅[调试时检查 XAML 属性](../debugger/inspect-xaml-properties-while-debugging.md)。  
  
  **预览实时可视化树中的所选元素**  
  选定了其上下文的 XAML 元素在“实时可视化树”窗口中也会被选中。  
  
  **在应用程序中显示运行时工具**  
  如果选中一个 XAML 元素的上下文，同时会在“实时可视化树”窗口中选中该元素。 Visual Studio 2015 Update 2 中引入了此选项。  
  
  **调试时启用诊断工具**  
  调试时显示“诊断工具”窗口。 有关详细信息，请参阅[调试器集成的分析](/visualstudio/profiling/running-profiling-tools-with-or-without-the-debugger)。  
  
  **在调试时显示运行时间 Perftips**  
  在进行调试时，代码窗口会显示给定方法调用的运行时间。  
  
  **启用 "编辑并继续"**  
  在进行调试时，你可以使用“编辑并继续”功能。  
  
  **启用本机编辑并继续**  
  在调试本机 C++ 代码时，你可以使用“编辑并继续”功能。 有关详细信息，请参阅[编辑并继续 (Visual C++)](../debugger/edit-and-continue-visual-cpp.md)。  
  
  **继续应用更改（仅限本机）**  
  从中断状态中恢复并继续执行进程时，Visual Studio 会自动编译并应用任何待执行的代码更改。 如果未选中，你可以选择使用调试菜单下的“应用代码更改”项来应用更改。  
  
  **警告过时代码（仅限本机）**  
  收到关于陈旧代码的警告。  
  
  **允许预编译（仅限本机）**  
  允许预编译。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)
