---
title: 如何：使用调用堆栈窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.callstack
dev_langs:
- FSharp
- VB
- CSharp
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
caps.latest.revision: 45
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 84c0bfead1633da13b4284cad04ace674045b057
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697473"
---
# <a name="how-to-use-the-call-stack-window"></a>如何：使用调用堆栈窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用“调用堆栈”窗口可以查看当前堆栈上的函数或过程调用。  
  
 **调用堆栈**窗口中显示的每个函数和编程语言中编写的名称。 函数或过程名称可能包含可选信息，如模块名称、行号、参数名称、类型和值。 可以打开或关闭这些可选信息的显示。  
  
 一个黄色箭头标识执行指针当前所位于的堆栈帧。 默认情况下，这是在源中，将显示其信息的帧**反汇编**，**局部变量**，**监视**，以及**自动**windows。 如果你想要将上下文更改为堆栈上的另一个帧，可以执行的操作**调用堆栈**窗口。  
  
 当调试符号不可用的一部分调用堆栈时**调用堆栈**窗口可能不能显示那部分调用堆栈的正确信息。 将出现以下表示法：  
  
 [下面的帧可能不正确和/或缺失，没有为 name.dll 加载符号]  
  
 在托管代码中，默认情况下。 **调用堆栈**窗口将隐藏非用户代码的信息。 在隐藏信息处出现以下表示法：  
  
 **[\<External Code>]**  
  
 非用户代码是任何代码，这些代码不是可通过快捷菜单选择以显示非用户代码的调用堆栈信息的我的代码。  
  
 可以使用快捷菜单选择查看线程之间的调用。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-display-the-call-stack-window-in-break-mode-or-in-run-mode"></a>以中断模式或运行模式显示“调用堆栈”窗口  
  
- 上**调试**菜单中，选择**Windows** ，然后单击**调用堆栈**。  
  
### <a name="to-change-the-optional-information-displayed"></a>更改显示的可选信息  
  
- 右键单击**调用堆栈**窗口和设置或清除**显示\<** _所需的信息_**>**.  
  
### <a name="to-display-non-user-code-frames-in-the-call-stack-window"></a>在“调用堆栈”窗口中显示非用户代码帧  
  
- 右键单击“调用堆栈”窗口，然后选择“显示外部代码”。  
  
### <a name="to-switch-to-another-stack-frame"></a>切换到另一个堆栈帧  
  
1. 在中**调用堆栈**窗口中，右键单击该帧其代码和您想要查看的数据。  
  
2. 选择“切换到帧”。  
  
     一个带有卷尾的绿色箭头显示在所选帧旁。 执行指针保留在原始帧中，仍然用黄色箭头标记。 如果从“调试”菜单中选择“单步执行”或“继续”，执行将继续在原始帧中进行，而不是在选定的帧中进行。  
  
### <a name="to-display-calls-to-or-from-another-thread"></a>显示与其他线程之间的来回调用  
  
- 右键单击“调用堆栈”窗口，然后选择“包括对其他线程和来自其他线程的调用”。  
  
### <a name="to-view-the-source-code-for-a-function-on-the-call-stack"></a>查看调用堆栈上的函数的源代码  
  
- 在“调用堆栈”窗口中，右键单击要查看其源代码的函数，然后选择“转到源代码”。  
  
### <a name="to-visually-trace-the-call-stack"></a>直观地跟踪调用堆栈  
  
1. 在“调用堆栈”窗口中，打开快捷菜单。 选择**在代码图上显示调用堆栈**。 （键盘：**CTRL** + **SHIFT** + **`**)  
  
     请参阅[调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。  
  
### <a name="to-view-the-disassembly-code-for-a-function-on-the-call-stack"></a>查看调用堆栈上的函数的反汇编代码  
  
- 在“调用堆栈”窗口中，右键单击要查看其反汇编代码的函数，然后选择“转到反汇编”。  
  
### <a name="to-run-to-a-specific-function-from-the-call-stack-window"></a>从“调用堆栈”窗口运行到特定函数  
  
- 在中**调用堆栈**窗口中，选择函数，右键单击并选择**运行到光标处**。  
  
### <a name="to-set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>在函数调用的退出点上设置断点  
  
- 请参阅[的调用堆栈函数处设置断点](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_the_call_stack_window)。  
  
### <a name="to-load-symbols-for-a-module"></a>加载模块符号  
  
- 在中**调用堆栈**窗口中，右键单击显示该模块的符号的帧，你想要重新加载，然后选择**加载符号**。  
  
## <a name="loading-symbols"></a>加载符号  
 在“调用堆栈”窗口中，可以为当前还未加载符号的代码加载调试符号。 这些符号可以是从 Microsoft 公共符号服务器下载的 .NET Framework 符号或系统符号，也可以是正在调试的计算机上的某个符号路径中的符号。  
  
 请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)  
  
#### <a name="to-load-symbols"></a>加载符号  
  
1. 在中**调用堆栈**窗口中，右键单击未加载符号的帧。 此帧将显示为灰色。  
  
2. 指向**负载从符号**，然后单击**Microsoft 符号服务器**或**符号路径**。  
  
#### <a name="to-set-the-symbol-path"></a>设置符号路径  
  
1. 在“调用堆栈”窗口中，从快捷菜单中选择“符号设置”。  
  
     “选项”对话框随即打开并显示“符号”页。  
  
2. 单击**符号设置**。  
  
3. 在“选项”对话框中单击“文件夹”图标。  
  
     “符号文件(.pdb)位置”框中随即出现一个光标。  
  
4. 键入所调试的计算机上的符号位置的目录路径名。 对于本地调试，此计算机指您的本地计算机。 对于远程调试，此计算机指远程计算机。  
  
5. 单击“确定”关闭“选项”对话框 。  
  
## <a name="see-also"></a>请参阅  
 [混合的代码与调用堆栈窗口中缺少的信息](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)   
 [如何：更改调试器 Windows 的数字格式](https://msdn.microsoft.com/library/cd593847-a625-411d-a430-b798346ef18f)   
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)   
 [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [使用断点](../debugger/using-breakpoints.md)
