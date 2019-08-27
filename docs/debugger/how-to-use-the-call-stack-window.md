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
ms.openlocfilehash: 2673ed9a69a80b2e9ab9275ff54909e33e4434f4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62906339"
---
# <a name="view-the-call-stack-and-use-the-call-stack-window-in-the-debugger"></a>查看调用堆栈，并使用调试器中的调用堆栈窗口

使用“调用堆栈”窗口可以查看当前堆栈上的函数或过程调用。 “调用堆栈”窗口显示方法和函数被调用的顺序。 调用堆栈是检查和理解应用执行流的好方法。

当[调试符号](#bkmk_symbols)不可用的一部分调用堆栈**调用堆栈**窗口可能不能显示那部分调用堆栈，改为显示正确的信息：

`[Frames below may be incorrect and/or missing, no symbols loaded for name.dll]`

> [!NOTE]
> “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图。

> [!NOTE]
> 显示的对话框和菜单命令可能与此处的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。  请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="view-the-call-stack-while-in-the-debugger"></a>查看调试器中的调用堆栈

- 在调试时，在**调试**菜单中，选择**Windows > 调用堆栈**。

  ![调用堆栈窗口](../debugger/media/dbg_basics_callstack_window.png "CallStackWindow")

一个黄色箭头标识执行指针当前所位于的堆栈帧。 默认情况下，此堆栈帧的信息会显示在源中，**局部变量**，**自动**，**观看**，以及**反汇编**windows。 若要将调试器上下文更改为在堆栈上的另一个帧[切换到另一个堆栈帧](#bkmk_switch)。

## <a name="display-non-user-code-in-the-call-stack-window"></a>在调用堆栈窗口中显示非用户代码

- 右键单击“调用堆栈”窗口，然后选择“显示外部代码”。

非用户代码是时不显示任何代码[仅我的代码](../debugger/just-my-code.md)已启用。 在托管代码中，默认情况下隐藏非用户代码帧。 非用户代码帧代替出现以下表示法：

`[<External Code>]`

## <a name="bkmk_switch"></a> 切换到另一个堆栈帧 （更改调试器上下文）

1. 在中**调用堆栈**窗口中，右击堆栈帧的代码和您想要查看的数据。

    或者，可以双击中的帧**调用堆栈**窗口切换到该框架。

2. 选择“切换到帧”。

     所选的堆栈帧旁边会显示一个带有卷尾的绿色箭头。 执行指针保留在原始帧中，仍然用黄色箭头标记。 如果从“调试”菜单中选择“单步执行”或“继续”，执行将继续在原始帧中进行，而不是在选定的帧中进行。

## <a name="view-the-source-code-for-a-function-on-the-call-stack"></a>查看调用堆栈上的一个函数的源代码

- 在“调用堆栈”窗口中，右键单击要查看其源代码的函数，然后选择“转到源代码”。

## <a name="run-to-a-specific-function-from-the-call-stack-window"></a>从调用堆栈窗口运行到特定函数

- 在中**调用堆栈**窗口中，选择该函数中，右键单击，然后选择**运行到光标处**。

## <a name="set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>函数调用的退出点上设置断点

- 请参阅[的调用堆栈函数处设置断点](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_the_call_stack_window)。

## <a name="display-calls-to-or-from-another-thread"></a>显示调用到或从另一个线程

- 右键单击“调用堆栈”窗口，然后选择“包括对其他线程和来自其他线程的调用”。

## <a name="visually-trace-the-call-stack"></a>直观地跟踪调用堆栈

在 Visual Studio Enterprise （仅限），可以在调试时查看调用堆栈代码图。

- 在“调用堆栈”窗口中，打开快捷菜单。 选择**在代码图上显示调用堆栈**(**Ctrl** + **Shift** + **`**)。

    有关详细信息，请参阅[调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

![在代码图上显示调用堆栈](../debugger/media/dbg_basics_show_call_stack_on_code_map.gif "ShowCallStackOnCodeMap")

## <a name="view-the-disassembly-code-for-a-function-on-the-call-stack-c-c-visual-basic-f"></a>查看调用堆栈上的一个函数的反汇编代码 (C#， C++，Visual Basic 中， F#)

- 在“调用堆栈”窗口中，右键单击要查看其反汇编代码的函数，然后选择“转到反汇编”。

## <a name="change-the-optional-information-displayed"></a>更改显示的可选信息

- 在中右击**调用堆栈**窗口和设置或清除**显示\<** _所需的信息_**>**.

## <a name="bkmk_symbols"></a> 加载模块的符号 (C#， C++，Visual Basic 中， F#)

在“调用堆栈”窗口中，可以为当前还未加载符号的代码加载调试符号。 这些符号可以是从 Microsoft 公共符号服务器下载的 .NET Framework 符号或系统符号，也可以是正在调试的计算机上的某个符号路径中的符号。

请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

### <a name="to-load-symbols"></a>加载符号

1. 在中**调用堆栈**窗口中，右键单击未加载符号的堆栈帧。 此帧将显示为灰色。

2. 指向**加载符号**，然后选择**Microsoft 符号服务器**（如果可用），或浏览到符号路径。

### <a name="to-set-the-symbol-path"></a>设置符号路径

1. 在“调用堆栈”窗口中，从快捷菜单中选择“符号设置”。

     “选项”对话框随即打开并显示“符号”页。

2. 选择**符号设置**。

3. 在“选项”对话框中单击“文件夹”图标。

     “符号文件(.pdb)位置”框中随即出现一个光标。

4. 正在调试的计算机上输入符号位置的目录路径名。 对于本地和远程调试，这是在本地计算机上的路径。

5. 选择**确定**以关闭**选项**对话框。

## <a name="see-also"></a>请参阅

- [“调用堆栈”窗口中的混合代码与丢失信息](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [使用断点](../debugger/using-breakpoints.md)