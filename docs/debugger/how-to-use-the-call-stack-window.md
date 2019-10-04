---
title: 在调试器中查看调用堆栈 |Microsoft Docs
ms.custom: seodec18
ms.date: 10/29/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.callstack
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
- aspx
helpviewer_keywords:
- threading [Visual Studio], displaying calls to or from
- functions [debugger], viewing code on call stack
- disassembly code
- breakpoints, Call Stack window
- debugging [Visual Studio], switching to another stack frame
- debugging [Visual Studio], Call Stack window
- Call Stack window, viewing source code for functions on the call stack
- stack, switching stack frames
- Call Stack window, viewing disassembly code for functions on the call stack
ms.assetid: 5154a2a1-4729-4dbb-b675-db611a72a731
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d0b9fb6e809f1124a10a6a2b4e35bc59806787a6
ms.sourcegitcommit: 8a3545329a58e446672181cfed2083f850e1ad14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71814336"
---
# <a name="view-the-call-stack-and-use-the-call-stack-window-in-the-debugger"></a>查看调用堆栈并使用调试器中的 "调用堆栈" 窗口

使用“调用堆栈”窗口可以查看当前堆栈上的函数或过程调用。 “调用堆栈”窗口显示方法和函数被调用的顺序。 调用堆栈是检查和理解应用执行流的好方法。

当[调试符号](#bkmk_symbols)对部分调用堆栈不可用时，"**调用堆栈**" 窗口可能无法显示调用堆栈的正确信息，而是显示：

`[Frames below may be incorrect and/or missing, no symbols loaded for name.dll]`

> [!NOTE]
> “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图。

> [!NOTE]
> 显示的对话框和菜单命令可能与此处的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。  请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="view-the-call-stack-while-in-the-debugger"></a>在调试器中查看调用堆栈

- 调试过程中，在 "**调试**" 菜单中选择 " **Windows > 调用堆栈**"。

  "![调用堆栈" 窗口](../debugger/media/dbg_basics_callstack_window.png "CallStackWindow")

一个黄色箭头标识执行指针当前所位于的堆栈帧。 默认情况下，此堆栈帧的信息显示在 "源"、"**本地**" **、"自动"、** "**监视**" 和 "**反汇编**" 窗口中。 若要将调试器上下文更改为堆栈上的另一个帧，请[切换到另一个堆栈帧](#bkmk_switch)。

## <a name="display-non-user-code-in-the-call-stack-window"></a>在 "调用堆栈" 窗口中显示非用户代码

- 右键单击“调用堆栈”窗口，然后选择“显示外部代码”。

非用户代码是启用[仅我的代码](../debugger/just-my-code.md)时未显示的任何代码。 在托管代码中，默认情况下隐藏非用户代码框架。 以下表示法显示为非用户代码帧：

`[<External Code>]`

## <a name="bkmk_switch"></a>切换到另一个堆栈帧（更改调试器上下文）

1. 在 "**调用堆栈**" 窗口中，右键单击要查看其代码和数据的堆栈帧。

    或者，您可以在 "**调用堆栈**" 窗口中双击某一帧以切换到该框架。

2. 选择“切换到帧”。

     选定的堆栈帧旁边会出现一个带有大向尾的绿色箭头。 执行指针保留在原始帧中，仍然用黄色箭头标记。 如果从“调试”菜单中选择“单步执行”或“继续”，执行将继续在原始帧中进行，而不是在选定的帧中进行。

## <a name="view-the-source-code-for-a-function-on-the-call-stack"></a>查看调用堆栈上的函数的源代码

- 在“调用堆栈”窗口中，右键单击要查看其源代码的函数，然后选择“转到源代码”。

## <a name="run-to-a-specific-function-from-the-call-stack-window"></a>从 "调用堆栈" 窗口运行到特定函数

- 在 "**调用堆栈**" 窗口中，选择该函数，右键单击，然后选择 "**运行到光标处**"。

## <a name="set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>在函数调用的退出点上设置断点

- 请参阅[在调用堆栈函数处设置断点](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)。

## <a name="display-calls-to-or-from-another-thread"></a>显示与其他线程之间的调用

- 右键单击“调用堆栈”窗口，然后选择“包括对其他线程和来自其他线程的调用”。

## <a name="visually-trace-the-call-stack"></a>直观地跟踪调用堆栈

在 Visual Studio Enterprise （仅限）中，你可以在调试时查看调用堆栈的代码图。

- 在“调用堆栈”窗口中，打开快捷菜单。 选择 **"在代码图上显示调用堆栈"** （**Ctrl** + **Shift** +  **`** ）。

    有关详细信息，请参阅[调试时在调用堆栈上映射方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

![在代码图上显示调用堆栈](../debugger/media/dbg_basics_show_call_stack_on_code_map.gif "ShowCallStackOnCodeMap")

## <a name="view-the-disassembly-code-for-a-function-on-the-call-stack-c-c-visual-basic-f"></a>查看调用堆栈上的函数的反汇编代码（C#、 C++、Visual Basic、） F#

- 在“调用堆栈”窗口中，右键单击要查看其反汇编代码的函数，然后选择“转到反汇编”。

## <a name="change-the-optional-information-displayed"></a>更改显示的可选信息

- 右键单击 "**调用堆栈**" 窗口，然后设置或清除 "**显示 \<** _" 所需的信息_ **>** 。

## <a name="bkmk_symbols"></a>为模块加载符号（C#、 C++、Visual Basic） F#

在“调用堆栈”窗口中，可以为当前还未加载符号的代码加载调试符号。 这些符号可以是从 Microsoft 公共符号服务器下载的 .NET Framework 符号或系统符号，也可以是正在调试的计算机上的某个符号路径中的符号。

请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

### <a name="to-load-symbols"></a>加载符号

1. 在 "**调用堆栈**" 窗口中，右键单击未加载符号的堆栈帧。 此帧将显示为灰色。

2. 指向 "**加载符号**"，然后选择 " **Microsoft 符号服务器**（如果可用）"，或浏览到符号路径。

### <a name="to-set-the-symbol-path"></a>设置符号路径

1. 在“调用堆栈”窗口中，从快捷菜单中选择“符号设置”。

     “选项”对话框随即打开并显示“符号”页。

2. 选择 "**符号设置**"。

3. 在“选项”对话框中单击“文件夹”图标。

     “符号文件(.pdb)位置”框中随即出现一个光标。

4. 输入要调试的计算机上的符号位置的目录路径名。 对于本地和远程调试，这是本地计算机上的路径。

5. 选择 **"确定"** 以关闭 "**选项**" 对话框。

## <a name="see-also"></a>请参阅

- [“调用堆栈”窗口中的混合代码与丢失信息](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [使用断点](../debugger/using-breakpoints.md)