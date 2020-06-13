---
title: 在调试器中设置符号 (.pdb) 和源文件
description: 了解如何配置和管理 Visual Studio 中的符号和源文件
ms.custom: ''
ms.date: 10/31/2019
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Debugger.Native
- VS.ToolsOptionsPages.Debugger.Symbols
- vs.debug.options.Native
- vs.debug.nosymbols
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- source code
- .dbg files
- source code, managing
- symbols, managing
- .pdb files
- dbg files
- pdb files
- debugger
ms.assetid: 1105e169-5272-4e7c-b3e7-cda1b7798a6b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 19eed30074215b64301d7227e93ba6bf5b438d78
ms.sourcegitcommit: 2f64b3b231900018fceafb72b5a1c65140213a18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "84183759"
---
# <a name="specify-symbol-pdb-and-source-files-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>在 Visual Studio 调试器（C#、C++、Visual Basic、F#）中指定符号 (.pdb) 和源文件

程序数据库 ( *.pdb*) 文件（也称为符号文件）将项目源代码中的标识符和语句映射到已编译应用中的相应标识符和说明。 这些映射文件将调试器链接到源代码，以进行调试。

使用标准调试生成配置从 Visual Studio IDE 生成项目时，编译器会创建相应的符号文件。 本文介绍如何在 IDE 中管理符号文件，例如，如何[在调试器选项中指定符号的位置](#BKMK_Specify_symbol_locations_and_loading_behavior)，如何在调试时[检查符号加载状态](#work-with-symbols-in-the-modules-window)，以及如何[在代码中设置符号选项](#compiler-symbol-options)。

有关符号文件的详细说明，请参阅以下内容：

- [了解符号文件和 Visual Studio 符号设置](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)

- [为什么 Visual Studio 要求调试器符号文件必须与同时生成的二进制文件完全匹配？](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)

## <a name="how-symbol-files-work"></a>符号文件的工作方式

.pdb 文件保存调试和项目状态信息，使用这些信息可以对应用的调试配置进行增量链接。 在调试时，Visual Studio 调试器使用 .pdb 文件来确定两项关键信息：

* 要在 Visual Studio IDE 中显示的源文件名和行号。
* 在应用中停止的断点位置。

符号文件还会显示源文件的位置，以及要从中检索它们的服务器（可选）。

调试器只会加载与在生成应用时创建的 .pdb 文件完全匹配的 .pdb 文件（即原始 .pdb 文件或副本）  。 这样的[完全重复](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)是必需的，因为即使代码本身未更改，应用的布局也可能会更改。

> [!TIP]
> 要在项目源代码之外调试代码（如项目调用的 Windows 代码或第三方代码），则必须指定外部代码的 .pdb 文件（也可以是源文件）的位置，这些文件必须与应用中生成的文件完全匹配。

## <a name="symbol-file-locations-and-loading-behavior"></a>符号文件位置和加载行为

在 Visual Studio IDE 中调试项目时，调试器将自动加载位于项目文件夹中的符号文件。

> [!NOTE]
> 在远程设备上调试托管代码时，所有符号文件必须位于本地计算机上，或者位于[调试器选项中指定](#BKMK_Specify_symbol_locations_and_loading_behavior)的位置。

调试器还会在以下位置搜索符号文件：

1. 在 DLL 或可执行 (.exe) 文件中指定的位置。

   默认情况下，如果你在计算机上已生成 DLL 或 .exe 文件，则链接器会将关联的 .pdb 文件的完整路径和文件名放入 DLL 或 .exe 文件中  。 调试器会检查该位置是否存在符号文件。

2. 与 DLL 或 .exe 文件相同的文件夹。

3. 在调试器选项中为符号文件指定的任何位置。 要添加并启用符号位置，请参阅[配置符号位置和加载选项](#BKMK_Specify_symbol_locations_and_loading_behavior)。

   - 任何本地符号缓存文件夹。

   - 指定的网络、Internet 或本地符号服务器和位置，例如 Microsoft 符号服务器（如果选择）。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 可从实现 `symsrv` 协议的符号服务器下载调试符号文件。 [Visual Studio Team Foundation Server](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols) 和 [Windows 调试工具](/windows-hardware/drivers/debugger/index)是可使用符号服务器的两个工具。

     可能会用到的符号服务器包括：

     **公共 Microsoft 符号服务器**：要调试在调用系统 DLL 或第三方库时出现的故障，通常需要系统 .pdb 文件。 系统 .pdb 文件包含 Windows DL、.exe 文件和设备驱动程序的符号 。 你可以从公共 Microsoft 符号服务器获取 Windows 操作系统、MDAC、IIS、ISA 和 .NET 的符号。

     **内部网络或本地计算机上的符号服务器**：你的团队或公司可为你自己的产品创建符号服务器，并作为外部源符号的缓存。 你自己的计算机上可能具有符号服务器。

     **第三方符号服务器**：Windows 应用程序和库的第三方提供程序可提供对 Internet 上的符号服务器的访问。

     > [!WARNING]
     > 如果使用公共 Microsoft 符号服务器以外的符号服务器，请确保该符号服务器及其路径是可信任的。 由于符号文件可以包含任意可执行代码，因此你可能面临安全威胁。

<a name="BKMK_Specify_symbol_locations_and_loading_behavior"></a>
### <a name="configure-symbol-locations-and-loading-options"></a>配置符号位置和加载选项

在“工具” > “选项” > “调试” > “符号”页面，你可以执行以下操作：   

- 为 Microsoft、Windows 或第三方组件指定和选择搜索路径和符号服务器。
- 指定你希望或不希望调试器自动为其加载符号的模块。
- 在主动调试时更改这些设置。 请参阅[调试时管理符号](#manage-symbols-while-debugging)。

**指定符号位置和加载选项：**

1. 在 Visual Studio 中，打开“工具” > “选项” > “调试” > “符号”（或“调试” > “选项” > “符号”）      。

2. 在“符号文件(.pdb)位置”下，
   - 要使用“Microsoft 符号服务器”或“NuGet.org 符号服务器”，请选中相应的复选框 。

   - 要添加新的符号服务器位置，请执行以下操作：
     1. 选择工具栏中的 + 符号。
     1. 在文本字段中键入 URL (http)、网络共享以及符号服务器或符号位置的本地路径。 语句结束有助于找到正确的格式。

     ![“工具”-“选项”-“调试”-“符号”页面](media/dbg-options-symbols.gif "“工具”-“选项”-“调试”-“符号”页面")

     >[!NOTE]
     >仅搜索指定的文件夹。 必须为要搜索的任何子文件夹添加条目。

   - 要添加新的 VSTS 符号服务器位置，请执行以下操作：
     1. 选择工具栏中的 ![“工具”-“选项”-“调试”-“符号”新服务器](media/dbg_tools_options_foldersicon.png "“工具”-“选项”-“调试”-“符号”新服务器图标") 图标。
     1. 在“连接到 VSTS 符号服务器”对话框中，选择一个可用的符号服务器，并选择“连接” 。

   - 要更改符号位置的加载顺序，请使用 Ctrl+向上和 Ctrl+向下箭头图标，或者使用向上和向下箭头图标     。
   - 要编辑 URL 或路径，请双击该条目，或者将其选中后按 F2。
   - 要删除某个条目，请将其选中，然后选择 - 图标。

3. （可选）要改进符号加载性能，请在“将符号缓存在此目录中”下，键入符号服务器可以将符号复制到的本地文件夹路径。

   > [!NOTE]
   > 不要将本地符号缓存放在一个受保护的文件夹中（例如 C:\Windows 或子文件夹）。 而应使用可读写的文件夹。

   > [!NOTE]
   > 对于 C++ 项目，如果已设置 `_NT_SYMBOL_PATH` 环境变量，它会覆盖“将符号缓存在此目录中”下设置的值。

4. 指定你希望调试器在启动时从“符号文件(.pdb)位置”加载的模块。

   - 选择“除排除模块之外的所有模块”（默认值），以便加载符号文件位置中所有模块（特别排除的模块除外）的所有符号。 要排除某些模块，请选择“指定排除的模块”，选择 + 图标，键入要排除的模块的名称，然后选择“确定”  。

   - 要仅加载从符号文件位置指定的模块，请选择“仅加载指定的模块”。 选择“指定包含的模块”，选择 + 图标，键入要包含的模块的名称，然后选择“确定”  。 这样便不会加载其他模块的符号文件。

5. 选择“确定”。

## <a name="other-symbol-options-for-debugging"></a>用于调试的其他符号选项

你可以在“工具” > “选项” > “调试” > “常规”（或者“调试” > “选项” > “常规”）中选择其他符号选项：      

- **加载 dll 导出(限本机)**

  加载适用于 C/C++ 的 DLL 导出表。 有关详细信息，请参阅 [DLL 导出表](#use-dumpbin-exports)。 读取 DLL 导出信息会产生一些开销，因此默认情况下会关闭加载导出表的功能。 你还可以在 C/ C++ 生成命令行中使用 `dumpbin /exports`。

- **启用地址级调试**和**无可用源时显示反汇编**

  无法找到源或符号文件时，始终显示反汇编。

  ![“选项”/“调试”/“常规”反汇编选项](../debugger/media/dbg_options_general_disassembly_checkbox.png "“选项”/“调试”/“常规”反汇编选项")
  <a name="BKMK_Use_symbol_servers_to_find_symbol_files_not_on_your_local_machine"></a>
- **启用源服务器支持**

  如果本地计算机上没有源代码，或者 .pdb 文件与源代码不匹配，则使用源服务器来帮助调试应用。 源服务器接受文件请求并返回源代码管理中的实际文件。 源服务器使用名为 srcsrv.dll 的 DLL 来读取应用的 .pdb 文件 。 .pdb 文件包含指向源代码存储库的指针，以及用于从该存储库检索源代码的命令。

  通过在名为 srcsrv.ini 的文件中列出允许的命令，可以限制 srcsrv.ini 从应用的 .pdb 文件执行的命令  。 将 srcsrv.ini 文件与 srcsrv.dll 和 devenv.exe 放在同一文件夹中  。

  >[!IMPORTANT]
  >任意命令都可嵌入应用的 .pdb 文件中，因此请确保在 srcsrv.ini 文件中仅放入要执行的命令 。 任何尝试执行不在“srcsvr.ini”文件中的命令都将导致出现一个确认对话框。 有关详细信息，请参阅[安全警告：调试器必须执行不受信任的命令](../debugger/security-warning-debugger-must-execute-untrusted-command.md)。
  >
  >未对命令参数执行任何验证，因此请慎用受信任的命令。 例如，如果已在 srcsrv.ini 中列出 cmd.exe，则恶意用户可能会在 cmd.exe 上指定让命令变得危险的参数  。

  选择此项和所需的子项。 “允许源服务器中的部分信任程序集(仅限托管)”和“始终运行不受信任的源服务器命令并且不再提示”都会增大上述安全风险 。

  ![启用源服务器选项](../debugger/media/dbg_options_general_enablesrcsrvr_checkbox.png "DBG_Options_General_EnableSrcSrvr_checkbox")

## <a name="compiler-symbol-options"></a>编译器符号选项

当你使用标准调试生成配置从 Visual Studio IDE 生成项目时，C++ 和托管编译器将为你的代码创建相应的符号文件。 你还可以在代码中设置编译器选项。

### <a name="net-options"></a>.NET 选项

使用 /debug 进行生成以创建 .pdb 文件。 可以使用 **/debug:full** 或 **/debug:pdbonly**生成应用程序。 使用 **/debug:full** 进行生成可以生成可调试的代码。 使用 /debug:pdbonly 进行生成可以生成 .pdb 文件，但不会生成通知 JIT 编译器调试信息可用的 `DebuggableAttribute`。 如果想为不希望其成为可调试的发布版本生成 .pdb文件，请使用 /debug:pdbonly。 有关详细信息，请参阅 [/debug（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)或 [/debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug)。

### <a name="cc-options"></a>C/C++ 选项

- VC\<x>.pdb 和 \<project>.pdb 文件 

  使用 [/ZI 或 /Zi](/cpp/build/reference/z7-zi-zi-debug-information-format) 进行生成时，将创建适用于 C/C++ 的 .pdb 文件。 在 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 中，[/Fd](/cpp/build/reference/fd-program-database-file-name) 选项会命名编译器创建的 .pdb 文件。 使用 IDE 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中创建项目时，/Fd 选项将设置为创建一个名为 \<project>.pdb 的 .pdb 文件 。

  如果使用生成文件生成 C/C++ 应用程序，并指定 /ZI 或 /Zi（而不使用 /Fd），则编译器会创建两个 .pdb 文件  ：

  - VC\<x>.pdb，其中 \<x> 表示 Microsoft C++ 编译器版本，例如 VC11.pdb  

    VC\<x>.pdb 文件存储各个项目文件的所有调试信息，并保存在与项目生成文件相同的目录中。 每当创建项目文件时，C/C++ 编译器都会将调试信息合并到 VC\<x>.pdb 中。 因此，即使每个源文件都包含公共头文件（如 \<windows.h>），这些头中的 typedef 也仅存储一次，而不是存储在每个项目文件中。 插入的信息包括类型信息，但不包括函数定义等符号信息。

  - *\<project>.pdb*

    \<project>.pdb 文件存储项目的 .exe 文件的所有调试信息，并保存在 \debug 子目录中  。 \<project.pdb文件包含完整的调试信息（包括函数原型），而不仅仅是在 VC\<x>.pdb中找到的类型信息。

  VC\<x>.pdb 文件和 \<project>.pdb 文件都允许增量更新 。 链接器还在它创建的 .exe 或 .dll 文件中嵌入 .pdb 文件的路径  。

- <a name="use-dumpbin-exports"></a>DLL 导出表

  使用 `dumpbin /exports` 查看 DLL 导出表中可用的符号。 DLL 导出表中的符号信息有助于处理 Windows 消息、Windows 过程 (WindowProc)、COM 对象、封送或不具有其符号的任何 DLL。 符号可用于任何 32 位系统 DLL。 调用将按调用顺序列出，当前函数（嵌套最深的函数）位于顶端。

  通过读取 `dumpbin /exports` 输出，可以查看到精确的函数名，包括非字母数字字符。 查看精确函数名有助于在函数上设置断点，因为函数名可能会在调试器的其他位置截断。 有关详细信息，请参阅 [dumpbin /exports](/cpp/build/reference/dash-exports)。

### <a name="web-applications"></a>Web 应用程序

将 ASP.NET 应用程序的 web.config 文件设置为调试模式。 调试模式将导致 ASP.NET 为动态生成的文件生成符号，并允许调试器附加到 ASP.NET 应用程序。 如果项目是通过 Web 项目模板创建的，则 Visual Studio 会在你开始调试时自动完成此设置。

## <a name="manage-symbols-while-debugging"></a>调试时管理符号

你可以使用“模块”、“调用堆栈”、“本地”、“自动”或任何“监视”窗口在调试时加载符号或更改符号选项    。 有关详细信息，请参阅[熟悉调试器如何附加到应用](../debugger/debugger-tips-and-tricks.md#modules_window)。

### <a name="work-with-symbols-in-the-modules-window"></a>在“模块”窗口中处理符号

调试过程中，“模块”窗口会显示调试器视为用户代码（即我的代码）的代码模块以及其符号加载状态。 你还可以在“模块”窗口中监视符号加载状态、加载符号以及更改符号选项。

**要在调试时监视或更改符号位置或选项：**

1. 若要在调试期间打开“模块”窗口，请选择“调试” > “窗口” > “模块”。
1. 在“模块”窗口中，右键单击“符号状态”或“符号文件”标头，或单击任意模块  。
1. 在上下文菜单中，选择以下选项之一：

|选项|描述|
|------------|-----------------|
|**加载符号**|对于具有跳过、未找到或未加载符号的模块显示。 尝试从“选项” > “调试” > “符号”页面中指定的位置加载符号  。 如果未找到或未加载符号文件，则启动“文件资源管理器”，以便你能够指定要搜索的新位置。|
|**符号加载信息**|显示已加载符号文件的位置或调试器无法找到文件时已搜索的位置。|
|**符号设置**|打开“选项” > “调试” > “符号”页面，你可以在其中编辑和添加符号位置  。|
|**始终自动加载**|将所选符号文件添加到由调试器自动加载的文件列表中。|

### <a name="use-the-no-symbols-loadedno-source-loaded-pages"></a>使用“未加载符号/未加载源”页面

调试器可通过多种方式中断没有可用符号或源文件的代码：

- 单步执行代码。
- 通过断点或异常中断代码。
- 切换到其他线程。
- 通过在“调用堆栈”窗口中双击堆栈帧来更改。

出现上述情况时，调试器将显示“未加载符号”页面或“未加载源”页面，以帮助你查找和加载必需的符号或源 。

 ![“未加载符号”页面](../debugger/media/dbg-nosymbolsloaded.png "DBG_NoSymbolsLoaded")

**使用“未加载符号”文档页面来帮助查找并加载缺少的符号：**

- 要更改搜索路径，请选择未选定的路径，或者选择“新路径”或“新 VSTS 路径”，然后输入或选择一个新路径 。 选择“加载”以再次搜索路径，并在找到符号文件时加载相应文件。
- 要覆盖任何符号选项并重试搜索路径，请选择“浏览并查找 \<executable-name>”。 如果找到了符号文件，则会加载该文件，否则将打开“文件资源管理器”，以便你手动选择符号文件。
- 要打开“选项” > “调试” > “符号”页面，请选择“更改符号设置”   。
- 要在新窗口中显示一次反汇编，请选择“查看反汇编”，或选择“选项”对话框，以便设置在找不到源或符号文件时始终显示反汇编的选项 。
- 要显示已搜索的位置和结果，请展开“符号加载信息”。

如果在执行其中一个选项后调试器找到 .pdb 文件，并且调试器可以使用 .pdb 文件中的信息检索源文件，则将显示源 。 否则，它会显示“未加载源”页面，页面中描述了问题并提供了指向可能解决该问题的操作链接。

**将源文件搜索路径添加到解决方案：**

你可以指定调试器搜索源文件的位置，并从搜索中排除特定的文件。

1. 在“解决方案资源管理器”中选择解决方案，然后选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”    。

1. 选择“调试源文件”。

1. 在“包含源代码的目录”中，键入或选择要搜索的源代码位置。 使用“新建行”图标可添加更多位置，使用向上和向下箭头图标可对这些位置重新排序，使用 X 图标可删除这些位置   。

   >[!NOTE]
   >调试器只搜索指定的目录。 你必须为要搜索的任何子目录添加项。

1. 在“不查找这些源文件”中，键入要从搜索中排除的源文件的名称。

1. 选择“确定”或“应用” 。

## <a name="see-also"></a>请参阅
- [了解符号文件和 Visual Studio 符号设置](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)

- [Visual Studio 2012 和 2013 中的 .NET 远程符号加载更改](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)
