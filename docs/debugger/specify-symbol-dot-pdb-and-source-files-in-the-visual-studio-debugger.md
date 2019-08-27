---
title: 在调试器中设置符号 (.pdb) 和源文件
ms.custom: seodec18
ms.date: 10/08/2018
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
ms.openlocfilehash: 2f2343d71d2ed0745f9c5a2a799c3018a2e64945
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746257"
---
# <a name="specify-symbol-pdb-and-source-files-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>在 Visual Studio 调试器中指定符号 (.pdb) 和源文件 (C#， C++，Visual Basic 中， F#)

程序数据库 ( *.pdb*) 文件，也称为符号文件将标识符映射和编译应用到相应的标识符的项目的源代码中的语句和中的说明。

从标准调试生成配置与 Visual Studio IDE 生成项目时，编译器会创建相应的符号文件。 此外可以[在代码中设置符号选项](#compiler-symbol-options)。

*.Pdb*文件保存调试和项目进行增量链接您的应用程序的调试配置的状态信息。 使用 Visual Studio 调试器 *.pdb*文件，以确定两个关键信息进行调试时：

* 源文件名和行号显示在 Visual Studio IDE 中。
* 若要针对某个断点停止在应用中的位置。

符号文件还显示源文件，和 （可选） 服务器来检索从它们的位置。

调试器仅加载 *.pdb*完全匹配的文件 *.pdb*生成应用时创建的文件 (即，原始 *.pdb*文件或副本)。 此确切的重复项是必需的因为即使代码本身未更改，可更改应用的布局。 有关详细信息，请参阅 [为什么 Visual Studio 要求调试器符号文件必须与同时生成的二进制文件完全匹配？](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)

> [!TIP]
> 若要调试项目源代码，之外的代码，如 Windows 代码或第三方代码项目调用，必须指定的外部代码的位置 *.pdb*文件 （和 （可选） 在源代码文件），其必须完全匹配应用程序中生成。

## <a name="symbol-file-locations-and-loading-behavior"></a>符号文件位置和加载行为

> [!NOTE]
> 调试在远程设备上的托管的代码时，所有符号文件都必须位于本地计算机上或在一个位置[调试器选项中指定](#BKMK_Specify_symbol_locations_and_loading_behavior)。

当调试 Visual Studio IDE 中的项目时，调试器会自动加载位于项目文件夹中的符号文件。

调试器还搜索符号文件位于以下位置：

1. 在 DLL 或可执行文件中指定的位置 ( *.exe*) 文件。

   默认情况下，如果已生成 DLL 或 *.exe*文件在计算机上，链接器将放的完整路径和文件名关联 *.pdb* DLL 中的文件或 *.exe*文件。 调试器将检查以查看在该位置中是否存在符号文件。

2. 与 DLL 相同的文件夹或 *.exe*文件。

3. 指定符号文件的调试器选项中任何位置。 若要添加并启用符号位置，请参阅[配置符号位置和加载选项](#BKMK_Specify_symbol_locations_and_loading_behavior)。

   - 任何本地符号缓存文件夹。

   - 如果选择，指定网络、 internet 或本地符号服务器和位置，例如 Microsoft 符号服务器。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 可以从实现的符号服务器下载调试符号文件`symsrv`协议。 [Visual Studio Team Foundation Server](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols)并[的 Windows 调试工具](/windows-hardware/drivers/debugger/index)是可以使用符号服务器的两个工具。

     可以使用符号服务器包括：

     **公共 Microsoft 符号服务器**:若要调试到系统 DLL 或第三方库的调用期间发生的故障，您通常需要系统 *.pdb*文件。 系统 *.pdb*文件包含 Windows Dll 符号 *.exe*文件和设备驱动程序。 您可以从公共 Microsoft 符号服务器获取的 Windows 操作系统、 MDAC、 IIS、 ISA、 和.NET Framework 的符号。

     **内部网络或本地计算机上的符号服务器**：你的团队或公司可为你自己的产品创建符号服务器，并作为外部源符号的缓存。 你自己的计算机上可能具有符号服务器。

     **第三方符号服务器**：Windows 应用程序和库的第三方提供程序可提供对 Internet 上的符号服务器的访问。

     > [!WARNING]
     > 如果使用公共 Microsoft 符号服务器以外的符号服务器，请确保符号服务器及其路径是可信任。 由于符号文件可以包含任意可执行代码，则可以会面临安全威胁。

<a name="BKMK_Specify_symbol_locations_and_loading_behavior"></a>
### <a name="configure-symbol-locations-and-loading-options"></a>配置符号位置和加载选项

上**工具** > **选项** > **调试** > **符号**页上，你可以：

- 指定并选择为 Microsoft、 Windows 或第三方组件的搜索路径和符号服务器。
- 指定没有或不希望调试器自动加载符号的模块。
- 主动进行调试时更改这些设置。 请参阅[调试时管理符号](#manage-symbols-while-debugging)。

**若要指定符号位置和加载选项：**

1. 在 Visual Studio 中打开**工具** > **选项** > **调试** > **符号**（或**调试** > **选项** > **符号**)。

   ![工具&#45;选项&#45;调试&#45;符号页](media/dbg-options-symbols.png "工具&#45;选项&#45;调试&#45;符号页")

2. 下**符号文件 (.pdb) 位置**，
   - 若要使用**Microsoft 符号服务器**，选中该复选框。

   - 若要添加新的符号服务器位置，
     1. 选择 **+** 工具栏中的符号。
     1. 在文本字段中键入符号服务器或符号位置的 URL 或文件夹路径。 语句结束有助于找到正确的格式。

     >[!NOTE]
     >搜索指定的文件夹。 必须添加任何子文件夹，你想要搜索的项。

   - 若要添加新的 VSTS 符号服务器位置，
     1. 选择![工具&#47;选项&#47;调试&#47;符号新服务器图标](media/dbg_tools_options_foldersicon.png "工具&#45;选项&#45;调试&#45;符号新服务器图标")工具栏中的图标。
     1. 在中**连接到 VSTS 符号服务器**对话框中，选择一个可用的符号服务器，然后选择**Connect**。

   - 若要更改符号位置的加载顺序，请使用**Ctrl**+**向上**并**Ctrl**+**向下**，或**向上**并**向下**箭头图标。
   - 若要编辑 URL 或路径，请双击该注册表项，或选择它并按**F2**。
   - 要移除的项，选择它，并选择 **-** 图标。

3. （可选）若要改进符号加载性能下**在此目录下缓存符号**，可以复制符号服务器的本地文件夹路径到符号的类型。

   > [!NOTE]
   > 未将本地符号缓存放在受保护的文件夹，例如 C:\Windows 或子文件夹。 而应使用可读写的文件夹。

   > [!NOTE]
   > 有关C++项目，如果你有`_NT_SYMBOL_PATH`环境变量集，它将重写下设置的值**在此目录下缓存符号**。

4. 指定希望调试器将从加载的模块**符号文件 (.pdb) 位置**启动时。

   - 选择**加载所有模块，除非排除**（默认） 加载所有符号的符号文件位置，除非专门排除的模块中的所有模块。 若要排除某些模块，请选择**指定排除的模块**，选择 **+** 图标，键入要排除，并选择的模块的名称**确定**。

   - 若要加载符号文件位置从指定的模块，请选择**负载仅指定的模块**。 选择**指定包含的模块**，选择 **+** 图标，键入要包括，，然后选择的模块的名称**确定**。 未加载其他模块的符号文件。

5. 选择 **确定**。

## <a name="other-symbol-options-for-debugging"></a>用于调试的其他符号选项

你可以选择中的其他符号选项**工具** > **选项** > **调试** > **常规**(或**调试** > **选项** > **常规**):

- **加载 dll 导出(限本机)**

  加载 DLL 导出表的 C /C++。 有关详细信息，请参阅[DLL 导出表](#use-dumpbin-exports)。 读取 DLL 导出信息占用一些系统开销，因此加载导出表处于关闭状态默认情况下。 此外可以使用`dumpbin /exports`在 C /C++生成命令行。

- **启用地址级调试**和**显示反汇编源代码不可用**

  找不到源文件或符号文件时，始终显示反汇编。

  ![选项&#47;调试&#47;常规反汇编选项](../debugger/media/dbg_options_general_disassembly_checkbox.png "选项&#47;调试&#47;常规反汇编选项")
  <a name="BKMK_Use_symbol_servers_to_find_symbol_files_not_on_your_local_machine"></a>
- **启用源服务器支持**

  使用源服务器来帮助调试在应用程序时在本地计算机上没有源代码或 *.pdb*文件与源代码不匹配。 源服务器接受文件请求并从源代码管理返回的实际文件。 源服务器运行通过使用名为的 DLL *srcsrv.dll*读取应用程序的 *.pdb*文件。 *.Pdb*文件包含指向源代码存储库，以及用来从存储库检索源代码的命令。

  可以限制命令的*srcsrv.dll*可从应用程序的执行 *.pdb*通过列出的允许的命令在名为的文件中的文件*srcsrv.ini*。 位置*srcsrv.ini*所在的同一文件夹中的文件*srcsrv.dll*并*devenv.exe*。

  >[!IMPORTANT]
  >任意命令都可以在应用中的嵌入 *.pdb*文件中，因此请确保将你想要执行到命令*srcsrv.ini*文件。 任何尝试执行不在“srcsvr.ini”文件中的命令都将导致出现一个确认对话框  。 有关详细信息，请参阅[安全警告：调试器必须执行不受信任的命令](../debugger/security-warning-debugger-must-execute-untrusted-command.md)。
  >
  >未对命令参数执行任何验证，因此请慎用受信任的命令。 例如，如果列表中，你*cmd.exe*在你*srcsrv.ini*，恶意用户可能会在上指定参数*cmd.exe*那样会使危险。

  选择此项和所需的子项目。 **允许源服务器中的部分信任程序集 （仅限托管）** 并**始终运行不受信任的源服务器命令并且不再提示**会增加安全风险。

  ![启用源服务器选项](../debugger/media/dbg_options_general_enablesrcsrvr_checkbox.png "DBG_Options_General_EnableSrcSrvr_checkbox")

## <a name="compiler-symbol-options"></a>编译器符号选项

从使用标准 Visual Studio IDE 生成项目时**调试**生成配置，C++和托管的编译器创建适当的符号文件为你的代码。 此外可以在代码中设置编译器选项。

### <a name="cc-options"></a>C/C++ 选项

- *VC\<x >.pdb*并 *\<项目 >.pdb*文件

  一个 *.pdb*于 c 语言的文件 /C++时使用生成创建[/ZI](/cpp/build/reference/z7-zi-zi-debug-information-format)。 在中[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]，则[/Fd](/cpp/build/reference/fd-program-database-file-name)选项名称 *.pdb*编译器创建的文件。 当你创建的项目中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]使用 IDE **/Fd**选项设置为创建 *.pdb*名为文件 *\<项目 >.pdb*。

  如果生成你的 C /C++应用程序使用的生成文件，并指定 **/ZI**或 **/Zi**而无需使用 **/Fd**，则编译器会创建两个 *.pdb*文件：

  - VC\<x >.pdb  ，其中 \<x >  表示 Visual C++ 版本，例如 VC11.pdb 

    *VC\<x >.pdb*文件存储为单独的对象文件中，所有调试信息并驻留在项目生成文件所在的同一目录中。 每次创建对象文件，C /C++编译器都会将合并到的调试信息*VC\<x >.pdb*。 因此，即使每个源文件包含公共头文件，如 *\<windows.h >* ，一次，而不是每个对象文件中存储这些标头中的 typedef。 插入的信息包括类型信息，但不包括函数定义等符号信息。

  - *\<project>.pdb*

    *\<项目 >.pdb*文件将存储项目的所有调试信息 *.exe*文件，并驻留在 *\debug*子目录。 \<project.pdb  文件包含完整的调试信息（包括函数原型），而不仅仅是在 VC\<x>.pdb  中找到的类型信息。

  这两个*VC\<x >.pdb*并 *\<项目 >.pdb*文件允许增量更新。 链接器还将嵌入到的路径 *.pdb*中的文件 *.exe*或 *.dll*它创建的文件。

- <a name="use-dumpbin-exports"></a>DLL 导出表

  使用`dumpbin /exports`若要查看 DLL 导出表中可用的符号。 DLL 导出表中的符号化信息也可用于处理 Windows 消息、 Windows 过程 (Windowproc)、 COM 对象、 封送处理，或不具有符号的任何 DLL。 符号可用于任何 32 位系统 DLL。 调用将按调用顺序列出，当前函数（嵌套最深的函数）位于顶端。

  通过阅读`dumpbin /exports`输出，您所见的确切函数名称，包括非字母数字字符。 查看确切的函数名称可用于设置断点的函数，因为可以在调试器中其他位置截断函数名称。 有关详细信息，请参阅 [dumpbin /exports](/cpp/build/reference/dash-exports)。

### <a name="net-framework-options"></a>.NET Framework 选项

使用生成 **/debug**来创建 *.pdb*文件。 可以使用 **/debug:full** 或 **/debug:pdbonly**生成应用程序。 使用 **/debug:full** 进行生成可以生成可调试的代码。 使用 /debug:pdbonly  进行生成可以生成 .pdb  文件，但不会生成通知 JIT 编译器调试信息可用的 `DebuggableAttribute`。 如果想为不希望其成为可调试的发布版本生成 .pdb  文件，请使用 /debug:pdbonly  。 有关详细信息，请参阅 [/debug（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)或 [/debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug)。

### <a name="web-applications"></a>Web 应用程序

设置*web.config*的 ASP.NET 应用程序，以调试模式下的文件。 调试模式将导致 ASP.NET 为动态生成的文件生成符号，并允许调试器附加到 ASP.NET 应用程序。 Visual Studio 自动完成此设置时开始调试，如果从 web 项目模板创建你的项目。

## <a name="manage-symbols-while-debugging"></a>调试时管理符号

可以使用**模块**，**调用堆栈**，**局部变量**，**自动**，或任何**监视**窗口加载符号或调试时更改符号选项。 有关详细信息，请参阅[更深入了解如何将调试器附加到您的应用程序](../debugger/debugger-tips-and-tricks.md#modules_window)。

### <a name="use-the-modules-window"></a>使用“模块”窗口

在调试期间，**模块**窗口显示了调试器将视为用户代码，或我的代码和其符号加载状态的代码模块。 此外可以监视符号加载状态、 加载符号，并更改符号选项在**模块**窗口。

**若要监视或调试时更改符号位置或选项：**

1. 若要在调试时打开**模块**窗口，选择**调试** > **窗口** > **模块**。
1. 在中**模块**窗口中，右键单击**符号状态**或**符号文件**标头或任何模块。
1. 在上下文菜单中，选择下列选项之一：

|选项|描述|
|------------|-----------------|
|**加载符号**|将显示为具有已跳过，找不到或未加载符号的模块。 尝试从上指定的位置加载符号**选项** > **调试** > **符号**页。 如果找不到或未加载符号文件，将启动**文件资源管理器**以便可以指定要搜索的新位置。|
|**符号加载信息**|显示加载的符号文件的位置或调试器无法找到该文件时已搜索的位置。|
|**符号设置**|此时将打开**选项** > **调试** > **符号**页上，在可以编辑和添加符号位置。|
|**始终自动加载**|将所选的符号文件添加到由调试器自动加载的文件的列表。|

### <a name="use-the-no-symbols-loadedno-source-loaded-pages"></a>使用 Loaded/No 源未加载任何符号页

调试器中断没有可用符号或源文件文件的代码，有多种：

- 单步执行代码。
- 中断代码通过断点或异常。
- 切换到不同的线程。
- 中双击帧来更改堆栈帧**调用堆栈**窗口。

在此情况下，调试器将显示**未加载任何符号**或**未加载任何源**页面，帮助你查找和加载必需的符号或源。

 ![没有未加载符号页](../debugger/media/dbg-nosymbolsloaded.png "DBG_NoSymbolsLoaded")

**若要使用的符号未加载任何文档页来帮助查找并加载缺少符号：**

- 若要更改搜索路径，请选择未选定的路径，或选择**新的路径**或**新建 VSTS 路径**并输入或选择一个新的路径。 选择**加载**以再次搜索路径并加载符号文件，如果找到，则为。
- 若要重写任何符号选项并重试搜索路径，请选择**浏览并查找\<可执行文件名称 >** 。 如果找到，则将加载符号文件或**文件资源管理器**打开，以便您可以手动选择符号文件。
- 若要打开**选项** > **调试** > **符号**页上，选择**更改符号设置**。
- 若要在新窗口中一次显示反汇编，请选择**查看反汇编**，或选择**选项对话框**设置选项以找不到源文件或符号文件时始终显示反汇编。
- 若要搜索的位置和结果显示，请展开**符号加载信息**。

如果调试器在找到 *.pdb*文件在执行其中一个选项，并可以检索使用中的信息的源文件之后 *.pdb*文件，它显示的源。 否则，将显示**未加载任何源**的页面，介绍的问题，可能会解决此问题的操作的链接。

**若要将源文件搜索路径添加到解决方案：**

可以指定调试器搜索源文件的位置，并从搜索中排除特定文件。

1. 选择中的解决方案**解决方案资源管理器**，然后选择**属性**图标中，按**Alt**+**Enter**，或右键单击并选择**属性**。

1. 选择**调试源文件**。

1. 下**目录包含源代码**，键入或选择要搜索的源位置。 使用**新行**图标以添加更多位置**向上**并**下**箭头图标，用于进行重新排序，或**X**图标以将其删除。

   >[!NOTE]
   >调试器将搜索指定的目录。 你必须为要搜索的任何子目录添加项。

1. 下**看起来不为这些源文件**，键入的源代码文件，以从搜索中排除的名称。

1. 选择**确定**或**应用**。

## <a name="see-also"></a>请参阅
- [了解符号文件和 Visual Studio 符号设置](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)

- [Visual Studio 2012 和 2013 中的 .NET 远程符号加载更改](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)
