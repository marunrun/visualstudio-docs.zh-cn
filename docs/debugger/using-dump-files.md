---
title: 使用在调试器中的转储文件 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/05/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.crashdump
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- dumps, about dumps
- crash dumps
- dump files
- dumps
ms.assetid: b71be6dc-57e0-4730-99d2-b540a0863e49
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f0b7edf8ef2670b70dbee25b70cac7b0597490b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65676361"
---
# <a name="dump-files-in-the-visual-studio-debugger"></a>在 Visual Studio 调试器中的转储文件

<a name="BKMK_What_is_a_dump_file_"></a> 一个*转储文件*是快照，显示已执行的过程和时间点应用的已加载的模块。 带有堆信息的转储此时还包括应用程序的内存的快照。

使用堆在 Visual Studio 中打开转储文件是类似于在调试会话中的断点处停止。 尽管你无法继续执行，但您可以在转储时检查堆栈、 线程和应用程序的变量值。

转储主要用于调试从开发人员无权访问的计算机的问题。 如果您无法重现崩溃或挂起自己的计算机上，可以使用从客户的计算机的转储文件。 测试人员还创建转储来保存故障或挂起数据以用于更多测试。

Visual Studio 调试器可为托管或本机代码保存转储文件。 它可以创建调试转储文件由 Visual Studio 或保存文件的其他应用*小型转储*格式。

## <a name="BKMK_Requirements_and_limitations"></a>要求和限制

- 若要调试 64 位计算机的转储文件，必须在 64 位计算机上运行 Visual Studio。

- Visual Studio 可以调试 ARM 设备中的本机应用程序的转储文件。 它还可以调试托管应用程序从 ARM 设备，但只是在本机调试器的转储。

- 若要调试[内核模式](/windows-hardware/drivers/debugger/kernel-mode-dump-files)转储文件，或使用[SOS.dll](/dotnet/framework/tools/sos-dll-sos-debugging-extension)调试扩展在 Visual Studio 中，下载适用于 Windows 中的调试工具[Windows Driver Kit (WDK)](/windows-hardware/drivers/download-the-wdk)。

- Visual Studio 无法调试转储文件保存在较旧[完整的用户模式转储](/windows/desktop/wer/collecting-user-mode-dumps)格式。 完整的用户模式转储不附带堆的转储相同。

- 调试优化过代码的转储文件可能让人困惑。 例如，函数的编译器内联可能产生意外的调用堆栈，而其他优化可能更改变量的生存期。

## <a name="BKMK_Dump_files__with_or_without_heaps"></a>带有或不带堆的转储文件

转储文件可能会或可能不包含堆信息。

- **转储文件的堆**包含应用程序的内存，包括变量的值在转储时的快照。 Visual Studio 还将在堆，可能会使调试变得更加容易的转储文件中加载的本机模块的二进制文件。 Visual Studio 可以从具有堆的转储文件中加载符号，即使它找不到应用程序二进制。

- **转储文件不带堆**比小得多转储与堆的方法，但调试器必须加载应用程序二进制文件，以查找符号信息。 加载二进制文件必须与转储创建过程中运行的完全匹配。 不带堆的转储文件保存仅堆栈变量的值。

## <a name="BKMK_Create_a_dump_file"></a>创建转储文件

当调试 Visual Studio 中的进程时，您可以在调试器已在异常或断点处停止时保存转储。

与[实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)启用，可以将 Visual Studio 调试器附加到 Visual Studio 外部的故障进程，然后将转储文件保存在调试器中。 请参阅[将附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

**保存转储文件：**

1. 在调试期间的错误或断点处停止时, 选择**调试** > **转储另存为**。

1. 在中**转储另存为**对话框中的**另存为类型**，选择**小型转储**或**附带堆信息的小型转储**（默认值）。

1. 浏览到的路径并选择转储文件的名称，然后选择**保存**。

>[!NOTE]
>可以使用支持 Windows 小型转储格式的任何程序创建转储文件。 例如，[Windows Sysinternals](https://technet.microsoft.com/sysinternals/default) 中的“Procdump”命令行实用工具可以基于触发器或按需创建进程故障转储文件。 请参阅[要求和限制](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations)有关使用其他工具创建转储文件的信息。

## <a name="BKMK_Open_a_dump_file"></a>打开转储文件

1. 在 Visual Studio 中，选择**文件** > **打开** > **文件**。

1. 在“打开文件”对话框中定位并选择转储文件。 它的扩展名通常为“.dmp”。 选择 **确定**。

   **小型转储文件摘要**窗口显示摘要和模块的信息的转储文件和操作可能需要。

   ![小型转储摘要页](../debugger/media/dbg_dump_summarypage.png "小型转储摘要页")

1. 下**操作**:
   - 若要设置正在加载位置的符号，请选择**设置符号路径**。
   - 若要开始调试，请选择**调试仅限托管**，**调试仅限本机**，**使用混合调试**，或**使用托管内存调试**。

## <a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a> 查找.exe、.pdb、 和源文件

若要使用完整的调试转储文件，按功能 Visual Studio 需要：

- *.Exe*创建转储时，文件和转储过程使用其他二进制文件 （Dll 等）。
- “.exe”的符号 (.pdb) 文件以及其他二进制文件。
- *.Exe*并 *.pdb*完全匹配的版本和生成处的文件的文件转储创建。
- 相关模块的源代码文件。 如果找不到源文件，可以使用模块的反汇编。

如果转储堆数据，Visual Studio 可以处理某些模块缺少二进制文件，但它必须具有足够多的模块来生成有效的调用堆栈的二进制文件。

### <a name="search-paths-for-exe-files"></a>.Exe 文件的搜索路径

Visual Studio 会自动搜索这些位置 *.exe*文件不包含在转储文件中：

1. 包含转储文件的文件夹。
2. 模块路径的转储文件指定，这是收集转储的计算机上的模块路径。
3. 中指定的符号路径**工具**(或**调试**) >**选项** > **调试** >  **符号**。 此外可以打开**符号**页上，从**操作**窗格**转储文件摘要**窗口。 在此页上，可以添加要搜索的多个位置。

### <a name="use-the-no-binary-no-symbols-or-no-source-found-pages"></a>使用无二进制、 无符号或未找到源页

如果 Visual Studio 找不到这些文件需要调试转储中的模块，它会显示**未找到二进制**，**未找到符号**，或**未找到源**页。 这些页面提供原因有关的问题的详细的信息，并提供操作链接，可帮助你找到的文件。 请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="see-also"></a>请参阅

- [实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)