---
title: “常规”&gt;“调试”&gt;“选项”对话框 | Microsoft Docs
ms.date: 11/12/2019
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
ms.openlocfilehash: 98bbd65d11b26d9b35000e4acbe4d28a585f8ddc
ms.sourcegitcommit: ce3d0728ec1063ab548dac71c8eaf26d20450acc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80472695"
---
# <a name="general-debugging-options"></a>常规调试选项

要设置 Visual Studio 调试器选项，请选择 **"工具** > **选项**"，并在 **"调试"** 下选择或取消选择 **"常规**"选项旁边的框。 您可以使用**工具** > **导入和导出设置** > 还原所有默认设置**重置所有设置**。 若要重置设置的子集，在做出要测试的更改之前，使用“导入和导出设置向导”保存设置，然后在以后导入保存的设置****。

可以设置以下“常规”选项****：

**删除所有断点之前，请询问**：在完成 **"删除所有断点"** 命令之前，需要确认。

**当一个进程中断时中断所有进程**：当发生中断时，同时中断将调试器附加到的所有进程。

**当异常跨越 AppDomain 或托管/本机边界时中断**：在托管或混合模式调试中，通用语言运行时可以捕获在以下条件为 true 时跨越应用程序域边界或托管/本机边界的异常：

1. 当本机代码使用 COM 互操作调用托管代码且托管代码引发异常。 请参阅 [COM 互操作介绍](/dotnet/articles/visual-basic/programming-guide/com-interop/introduction-to-com-interop)。

2. 应用程序域 1 中运行的托管代码调用应用程序域 2 中的托管代码，且应用程序域 2 中的代码引发异常。 请参阅[应用程序域编程](/dotnet/articles/framework/app-domains/index)。

3. 代码通过使用反射调用一个函数时且该函数引发异常。 请参阅[反射](/dotnet/framework/reflection-and-codedom/reflection)。

在 2 和 3 的情况下，异常有时由 `mscorlib` 中的托管代码而非由公共语言运行时捕获。 此选项不影响在 `mscorlib` 捕获到异常时中断。

**启用地址级调试**：启用用于在地址级别（**拆解**窗口、**寄存器**窗口和地址断点）进行调试的高级功能。

- **如果源不可用，请显示拆解**：在调试源不可用的代码时，自动显示 **"拆解**"窗口。

**启用断点筛选器**：使您能够在断点上设置筛选器，以便它们仅影响特定进程、线程或计算机。

**使用新的例外帮助程序**：启用替换异常助手的异常帮助程序。 （支持从 Visual Studio 2017 开始使用例外帮助程序）

> [!NOTE]
> 对于托管代码，此选项以前称为“启用异常助手”****。

**仅启用"我的代码**"：调试器仅显示和步骤到用户代码（"我的代码"），忽略系统代码和其他经过优化或没有调试符号的代码。

- **警告启动时没有用户代码（仅限托管）：** 当调试从启用的"仅我的代码"开始时，此选项将警告您如果没有用户代码（"我的代码"）。

**启用 .NET 框架源步长**：允许调试器步进 .NET 框架源。 启用此选项会自动禁用“仅我的代码”。 .NET Framework 符号将下载到缓存位置。 使用“选项”对话框>“调试类别”>“符号”页面可更改缓存位置************。

**跨步执行属性和运算符（仅限托管）：** 防止调试器步进托管代码中的属性和运算符。

**启用属性计算和其他隐式函数调用**：打开变量窗口中的属性和隐式函数调用的自动计算和隐式函数调用以及**QuickWatch**对话框。

- **在变量窗口（仅限 C# 和 JavaScript）中的对象上调用字符串转换函数**：在变量窗口中评估对象时执行隐式字符串转换调用。 结果显示为字符串而不是类型名称。 仅在 C# 代码中进行调试时适用。 此设置可能被调试器显示属性覆盖（请参阅[使用调试器显示属性](../debugger/using-the-debuggerdisplay-attribute.md)）。

**启用源服务器支持**：告诉 Visual Studio 调试器从实现 SrcSrv （`srcsrv.dll`） 协议的源服务器获取源文件。 Team Foundation Server 和 Windows 的调试工具是实现协议的两个源服务器。 有关 SrcSrv 设置的详细信息，请参阅[SrcSrv](/windows-hardware/drivers/debugger/srcsrv)文档。 此外，请参阅[指定符号 （.pdb） 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

> [!IMPORTANT]
> 因为读取 *.pdb*文件可以在文件中执行任意代码，因此请确保信任服务器。

- **将源服务器诊断消息打印到"输出"窗口**：启用源服务器支持时，此设置将打开诊断显示。

- **允许源服务器用于部分信任程序集（仅限托管）：** 启用源服务器支持时，此设置将覆盖不检索部分信任程序集的源的默认行为。

- **始终运行不受信任的源服务器命令，而不提示**：启用源服务器支持时，此设置将覆盖运行不受信任的命令时的默认提示行为。

**启用源链接支持**：告诉可视化工作室调试器下载包含源链接信息的 *.pdb*文件的源文件。 有关源链接的详细信息，请参阅[源链接规范](/dotnet/standard/library-guidance/sourcelink)。

> [!IMPORTANT]
> 由于源链接将使用 http 或 https 下载文件，因此请确保你信任该 .pdb** 文件。

- **回退到所有源链接请求的 Git 凭据管理器身份验证**：启用源链接支持，并且源链接请求失败身份验证时，Visual Studio 调用 Git 凭据管理器。

**突出显示断点和当前语句的整行（仅限C++）：** 当调试器突出显示断点或当前语句时，它会突出显示整行。

**要求源文件与原始版本完全匹配**：告诉调试器验证源文件是否与用于生成正在调试的可执行文件的源代码的版本匹配。 若版本不匹配，系统会提示你查找匹配的源。 如果未找到匹配源，则在调试过程中不会显示源代码。

**将所有输出窗口文本重定向到"立即"窗口**：将通常出现在 **"输出"** 窗口中的所有调试器消息发送到 **"立即"** 窗口。

**在变量窗口中显示对象的原始结构**：关闭所有对象结构视图自定义项。 有关视图自定义的详细信息，请参阅[创建托管对象的自定义视图](../debugger/create-custom-views-of-managed-objects.md)。

**在模块加载（仅限托管）上禁止 JIT 优化**：在加载模块时禁用托管代码的 JIT 优化，并在连接调试器时编译 JIT。 禁用优化可能更易于调试某些问题，尽管这会降低性能。 如果正在使用“仅我的代码”，则禁用 JIT 优化会导致非用户代码显示为用户代码（“我的代码”）。 有关详细信息，请参阅[JIT 优化和调试](../debugger/jit-optimization-and-debugging.md)。

**为ASP.NET（Chrome、微软边缘和 IE）启用 JavaScript 调试：** 启用ASP.NET应用的脚本调试器。 第一次在 Chrome 中使用时，可能需要登录到浏览器来启用已安装的 Chrome 扩展。 禁用此选项可还原为旧行为。

**为 UWP JavaScript 应用启用边缘开发人员工具（实验）：** 启用 Microsoft Edge 中 UWP JavaScript 应用的开发人员工具。

**为ASP.NET启用传统的 Chrome JavaScript 调试器**：为ASP.NET应用启用传统的 Chrome JavaScript 脚本调试器。 第一次在 Chrome 中使用时，可能需要登录到浏览器来启用已安装的 Chrome 扩展。

**使用实验方法启动 Chrome JavaScript 调试时运行 Visual Studio 作为管理员**： 告诉可视化工作室尝试在 JavaScript 调试期间启动 Chrome 的新方法。

**加载 dll 导出（仅限本机）：** 加载 dll 导出表。 处理 Windows 消息、Windows 过程 (WindowProc)、COM 对象、封送或不具有其符号的任何 DLL 时，DLL 导出表中的符号信息将很有用。 读取 DLL 导出信息会占用一些系统开销。 因此，默认情况下此功能被禁用。

若要查看 DLL 导出表中的可用符号，请使用 `dumpbin /exports`。 符号可用于任何 32 位系统 DLL。 从 `dumpbin /exports` 输出中，可以查看到精确的函数名，包括非字母数字字符。 这对于在函数上设置断点很有用。 DLL 导出表中的函数名在调试器的其他位置似乎被截断了。 调用将按调用顺序列出，当前函数（嵌套最深的函数）位于顶端。 有关详细信息，请参阅 [dumpbin /exports](/cpp/build/reference/dash-exports)。

**自下而上显示并行堆栈图**：控制堆栈在 **"并行堆栈**"窗口中显示的方向。

**如果写入的数据未更改值，请忽略 GPU 内存访问异常**：如果数据未更改，则忽略在调试过程中检测到的争用条件。 有关详细信息，请参阅[调试 GPU 代码](../debugger/debugging-gpu-code.md)。

**使用托管兼容性模式**：将默认调试引擎替换为旧版本以启用这些方案：

- 您使用的是提供其自己的表达式赋值器（包括C++/CLI）以外的 .NET 语言。C#、可视基本或 F#。

- 想要在混合模式调试过程中为 C++ 项目启用“编辑并继续”。

> [!NOTE]
> 选择托管兼容性模式会禁用仅在默认调试引擎中实现的某些功能。 旧版调试引擎在 Visual Studio 2012 中被替换。

**使用传统的 C# 和 VB 表达式赋值器**：调试器将使用 Visual Studio 2013 C# 或可视化基本表达式赋值器，而不是基于 Roslyn 的 Visual Studio 2015 表达式赋值器。

**在针对潜在的不安全进程（仅限托管）使用自定义调试器可视化器时发出警告**：当您使用在调试过程中运行代码的自定义调试器可视化器时，Visual Studio 会发出警告，因为它可能运行不安全的代码。

**启用 Windows 调试堆分配器（仅限本机）：** 启用 Windows 调试堆以改进堆诊断。 启用此选项会影响调试性能。

**为 XAML 启用 UI 调试工具**：当您开始**调试受支持**的项目类型时，将显示实时可视化树和实时属性浏览窗口。 有关详细信息，请参阅[调试时检查 XAML 属性](../xaml-tools/inspect-xaml-properties-while-debugging.md)。

- **预览实时可视化树中的选定元素**：其上下文被选中的 XAML 元素也在 **"实时可视化树"** 窗口中被选中。

- **在应用程序中显示运行时工具**：在正在调试的 XAML 应用程序的主窗口中的工具栏中显示**实时可视化树**命令。 此选项在 Visual Studio 2015 更新 2 中引入。

- **启用 XAML 热重新加载**：允许您在应用运行时使用 XAML 热重新加载功能与 XAML 代码。 （此功能以前称为"XAML 编辑并继续"）

::: moniker range=">= vs-2019" 
- **仅启用我的 XAML**： 从 Visual Studio 2019 版本 16.4 开始，默认情况下**的实时可视化树**仅显示归类为用户代码的 XAML。 如果禁用此选项，该工具中将显示所有生成的 XAML 代码。

- **选择元素时关闭选择模式**从 Visual Studio 2019 版本 16.4 开始，应用内工具栏元素选择器按钮 （**启用选择**） 在选择元素时关闭。 如果禁用此选项，元素选择将保持打开状态，直到您再次单击应用内工具栏按钮。
::: moniker-end

**调试时启用诊断工具**：调试时将显示**诊断工具**窗口。

**在调试时显示已用时间 PerfTip：** 代码窗口显示调试时给定方法调用的已用时间。

**启用编辑并继续**：在调试时启用"编辑并继续"功能。

- **启用本机编辑并继续**：您可以在调试本机C++代码时使用"编辑并继续"功能。 有关详细信息，请参阅[编辑并继续 （C++）](../debugger/edit-and-continue-visual-cpp.md)。

- **在继续时应用更改（仅限本机）：Visual**Studio 会自动编译并应用从中断状态继续进程时所做的任何未完成的代码更改。 如果未选中，则可以选择使用 **"调试"** 菜单下的 **"应用代码更改"项应用更改**。

- **警告过时代码（仅限本机代码）：** 获取有关过时代码的警告。

**调试时在编辑器中显示"运行到单击"按钮**：选择此选项时，调试时将显示["运行到单击"](../debugger/debugger-feature-tour.md#run-to-a-point-in-your-code-quickly-using-the-mouse)按钮。

**调试停止时自动关闭控制台**：告诉 Visual Studio 在调试会话结束时关闭控制台。

::: moniker range=">= vs-2019"
**启用快速表达式计算（仅限托管）：** 允许调试器通过模拟简单属性和方法的执行来尝试更快的计算。
::: moniker-end

## <a name="options-available-in-older-versions-of-visual-studio"></a>旧版本的 Visual Studio 提供选项

如果您使用的是旧版本的 Visual Studio，则可能存在一些其他选项。

**启用异常助理**：对于托管代码，启用异常助理。 从 Visual Studio 2017 开始，异常帮助程序替换了异常助手。

**解除未处理异常上的调用堆栈**：导致**调用堆栈**窗口将调用堆栈回滚到未处理异常发生之前的点。

**警告启动时没有符号（仅限本机）：** 在调试调试器没有符号信息的程序时显示警告对话框。

**警告在启动时脚本调试是否禁用**：在启动调试器时显示一个警告对话框，禁用脚本调试。

**使用本机兼容性模式**：选择此选项后，调试器使用 Visual Studio 2010 本机调试器，而不是新的本机调试器。

- 如果正在调试 .NET C++ 代码，请使用此选项，因为新的调试引擎不支持计算 .NET C++ 表达式。 但是，启用本机兼容模式会禁用依赖于当前调试器实现来操作的许多功能。 例如，旧引擎缺少许多用于内置类型（如 Visual Studio 2015 项目中的 `std::string`）的可视化工具。   为获得最佳调试体验，在这些应用场景中请使用 Visual Studio 2013 项目。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
