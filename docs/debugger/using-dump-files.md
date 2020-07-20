---
title: 在调试器中使用转储文件 | Microsoft Docs
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
ms.openlocfilehash: db6d4e8bc5b2f09194e03bbadc8f49b773d24f1e
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86386948"
---
# <a name="dump-files-in-the-visual-studio-debugger"></a>Visual Studio 调试器中的转储文件

<a name="BKMK_What_is_a_dump_file_"></a>转储文件是一个快照，其显示某个时间点正在为应用执行的进程和已为应用加载的模块。 带堆信息的转储还包括该时间点的应用内存的快照。

在 Visual Studio 中打开带堆的转储文件类似于在调试会话中在断点处停止。 尽管你无法继续执行，但在转储时可以检查应用的堆栈、线程和变量值。

转储最常用于调试开发人员无权访问的计算机中的问题。 当你无法在自己的计算机上重现崩溃或无响应的程序时，可以使用来自客户计算机的转储文件。 测试人员还会创建转储以保存崩溃或无响应程序数据，从而用于更多测试。

Visual Studio 调试器可为托管或本机代码保存转储文件。 它可以调试由 Visual Studio 或其他以小型转储格式保存文件的应用创建的转储文件。

## <a name="requirements-and-limitations"></a><a name="BKMK_Requirements_and_limitations"></a>要求和限制

- 若要调试来自 64 位计算机的转储文件，Visual Studio 必须在 64 位计算机上运行。

- Visual Studio 可以调试 ARM 设备中的本机应用程序的转储文件。 它还可以调试 ARM 设备中的托管应用的转储，但仅限于在本机调试器中。

- 若要在 Visual Studio 中调试[内核模式](/windows-hardware/drivers/debugger/kernel-mode-dump-files)转储文件或使用 [SOS.dll](/dotnet/framework/tools/sos-dll-sos-debugging-extension) 调试扩展，请下载 [Windows 驱动程序工具包 (WDK)](/windows-hardware/drivers/download-the-wdk) 中适用于 Windows 的调试工具。

- Visual Studio 无法调试以较旧的[完全用户模式转储](/windows/desktop/wer/collecting-user-mode-dumps)格式保存的转储文件。 完全用户模式转储与带堆的转储不同。

- 调试优化过代码的转储文件可能让人困惑。 例如，函数的编译器内联可能产生意外的调用堆栈，而其他优化可能更改变量的生存期。

## <a name="dump-files-with-or-without-heaps"></a><a name="BKMK_Dump_files__with_or_without_heaps"></a>带有或不带堆的转储文件

转储文件不一定具有堆信息。

- **带堆的转储文件**包含转储时的应用内存的快照，其中包括变量的值。 Visual Studio 还会在带堆的转储文件中保存加载的本机模块的二进制文件，这可让调试变得更加容易。 Visual Studio 可以从带堆的转储文件中加载符号，即使找不到应用二进制文件也是如此。

- **不带堆的转储文件**比带堆的转储要小得多，但调试器必须加载应用二进制文件才能查找符号信息。 加载的二进制文件必须与转储创建期间运行的二进制文件完全匹配。 不带堆的转储文件仅保存堆栈变量的值。

## <a name="create-a-dump-file"></a><a name="BKMK_Create_a_dump_file"></a>创建转储文件

在 Visual Studio 中调试进程时，你可以在调试器已在异常或断点处停止时保存转储。

启用[实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)后，可以将 Visual Studio 调试器附加到 Visual Studio 外部的崩溃进程，然后从调试器保存转储文件。 请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

**保存转储文件：**

1. 调试期间在错误或断点处停止时，选择“调试” > “将转储另存为”。

1. 在“将转储另存为”对话框中的“保存类型”下，选择“小型转储”或“附带堆信息的小型转储”（默认）。

1. 浏览到某个路径并选择转储文件的名称，然后选择“保存”。

>[!NOTE]
>你还可以使用支持 Windows 小型转储格式的任何程序创建转储文件。 例如，[Windows Sysinternals](https://technet.microsoft.com/sysinternals/default) 中的“Procdump”命令行实用工具可以基于触发器或按需创建进程故障转储文件。 有关使用其他工具创建转储文件的信息，请参阅[要求和限制](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations)。

## <a name="open-a-dump-file"></a><a name="BKMK_Open_a_dump_file"></a>打开转储文件

1. 在 Visual Studio 中，选择“文件” > “打开” > “文件”  。

1. 在“打开文件”对话框中定位并选择转储文件。 它的扩展名通常为“.dmp”。 选择“确定”。

   “小型转储文件摘要”窗口显示转储文件的摘要和模块信息，以及你可以执行的操作。

   ![小型转储摘要页](../debugger/media/dbg_dump_summarypage.png "小型转储摘要页")

1. 在“操作”下：
   - 若要设置符号加载位置，请选择“设置符号路径”。
   - 若要开始调试，请选择“仅调试托管内存”、“仅调试本机内存”、“调试混合型内存”或“调试托管内存”。

## <a name="find-exe-pdb-and-source-files"></a><a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a>查找 .exe、.pdb 和源文件

若要对转储文件使用完整的调试功能，Visual Studio 需要：

- 为其创建转储的 .exe 文件以及转储进程使用的其他二进制文件（DLL 等）。
- “.exe”的符号 (.pdb) 文件以及其他二进制文件 。
- 与创建转储时的文件版本和内部版本完全匹配的 .exe 和 .pdb 文件。
- 相关模块的源文件。 如果找不到源文件，则可以使用模块的反汇编。

如果转储带有堆数据，则 Visual Studio 可以处理某些模块缺少二进制文件的情况，但是它必须具有足够多的模块的二进制文件才能生成有效的调用堆栈。

### <a name="search-paths-for-exe-files"></a>搜索 .exe 文件的路径

Visual Studio 会自动搜索未包含在转储文件中的 .exe 文件的位置：

1. 包含转储文件的文件夹。
2. 转储文件指定的模块路径，即收集转储的计算机上的模块路径。
3. 在“工具”（或“调试”）>“选项” > “调试” > “符号”中指定的符号路径。 你也可以从“转储文件摘要”窗口的“操作”窗格中打开“符号”页。 在此页上，你可以添加更多要搜索的位置。

### <a name="use-the-no-binary-no-symbols-or-no-source-found-pages"></a>使用“未找到二进制文件”、“未找到符号”或“未找到源”页

如果 Visual Studio 在转储中找不到调试模块所需的文件，则会显示“未找到二进制文件”、“未找到符号”或“未找到源”页。 这些页面提供有关问题原因的详细信息，并提供可帮助找到文件的操作链接。 请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="see-also"></a>请参阅

- [实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)