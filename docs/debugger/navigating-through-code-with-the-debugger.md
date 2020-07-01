---
title: 使用调试器导航代码 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/12/2018
ms.topic: how-to
f1_keywords:
- vs.debug.execution
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 759072ba-4aaa-447e-8e51-0dd1456fe896
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5d6b9bb2eb6169de2bbbf41b6d4e96a5960e40fe
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348244"
---
# <a name="navigate-through-code-with-the-visual-studio-debugger"></a>使用 Visual Studio 调试器浏览代码

Visual Studio 调试器可帮助你浏览代码，以检查应用的状态并显示其执行流。 可以使用键盘快捷方式、调试命令、断点和其他功能来快速访问要检查的代码。 熟悉调试器导航命令和快捷方式有助于更快、更轻松地查找和解决应用问题。  如果是首次尝试调试代码，那么在阅读本文前，可能需要阅读[零基础调试](../debugger/debugging-absolute-beginners.md)和[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="get-into-break-mode"></a>进入“中断模式”

在“中断模式”中，应用执行被挂起，而函数、变量和对象保留在内存中。 调试器进入中断模式后，即可浏览代码。 快速进入中断模式的最常见方法包括：

- 通过按 F10 或 F11 开始单步执行代码。 这使你可以快速找到应用的入口点，然后可以继续按单步执行命令导航代码。

- [运行到特定位置或函数](#BKMK_Break_into_code_by_using_breakpoints_or_Break_All)，例如，通过[设置断点](using-breakpoints.md)并启动应用。

   例如，在 Visual Studio 的代码编辑器中，可以使用“运行到光标处”命令启动应用，附加调试器并进入中断模式，然后使用 F11 导航代码。

   ![运行到光标处并单步执行代码](../debugger/media/navigate-code-code-stepping.gif "运行到光标处并单步执行代码")

进入中断模式后，你可以使用各种命令浏览代码。 在中断模式下，你可以检查变量的值，以查找冲突或 bug。 对于某些项目类型，你还可以在中断模式下对应用进行调整。

大多数调试器窗口（例如“模块”和“监视”窗口）仅在将调试器附加到应用后才可用。 某些调试器功能（例如在“局部变量”窗口中查看变量值或在“监视”窗口中计算表达式）仅在调试器暂停时（即在中断模式下）可用。

> [!NOTE]
> 如果中断未加载源或符号 (.pdb) 文件的代码，调试器会显示“未找到源文件”或“未找到符号”页，这可帮助你查找和加载文件。 请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 如果无法加载符号或源文件，仍可以在“反汇编”窗口中调试汇编指令。

## <a name="step-through-code"></a>逐行执行代码

调试器单步执行命令可帮助检查应用状态或详细了解其执行流。

### <a name="step-into-code-line-by-line"></a><a name="BKMK_Step_into__over__or_out_of_the_code"></a>逐行单步执行代码

若要在调试时在每个语句上停止，请使用“调试” > “单步执行”，或按 F11。

调试器会逐句通过代码语句，而不是物理行。 例如，`if` 子句可以写在一行内：

  ```csharp
  int x = 42;
  string s = "Not answered";
  if( int x == 42) s = "Answered!";
  ```

  ```vb
  Dim x As Integer = 42
  Dim s As String = "Not answered"
  If x = 42 Then s = "Answered!"
  ```

但是，当你单步执行此行时，调试器将条件视为一步，将结果视为另一步。 在前面的示例中，条件为 true。

在嵌套函数调用上， **“逐语句”** 将进入并单步执行嵌套最深的函数。 例如，如果对类似 `Func1(Func2())` 的调用使用“单步执行”，调试器将单步执行函数 `Func2`。

>[!TIP]
>在执行每行代码时，你可以将鼠标悬停在变量上以查看其值，或使用 [局部变量](autos-and-locals-windows.md)和 [监视](watch-and-quickwatch-windows.md)窗口来观察值的变化。 还可以在单步执行函数的过程中直观地跟踪[调用堆栈](how-to-use-the-call-stack-window.md)。 （仅限 Visual Studio Enterprise，请参阅[调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)）。

### <a name="step-through-code-and-skip-some-functions"></a><a name="BKMK_Step_over_Step_out"></a>逐句通过代码并跳过某些函数

在调试时，你可能并不关心某个函数，或者你知道它可以正常工作，例如经过充分测试的库代码。 你可以在单步执行代码时使用以下命令跳过代码。 这些函数仍会执行，但调试器会跳过它们。

|键盘命令|调试菜单命令|描述|
|----------------------|------------------|-----------------|
|**F10**|**逐过程**|如果当前行包含函数调用，则“单步跳过”运行代码，然后在被调用函数返回后，在第一行代码处挂起执行。|
|Shift+F11|**跳出**|“单步跳出”继续运行代码，并在当前函数返回时挂起执行。 调试器跳过当前函数。|

## <a name="run-to-a-specific-location-or-function"></a><a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a>运行到特定位置或函数

当你确切知道要检查的代码或者知道要开始进行调试的位置时，你可能更想要直接运行到特定位置或函数。

### <a name="run-to-a-breakpoint-in-code"></a>运行到代码中的断点

若要在代码中设置简单的断点，请单击要挂起执行的代码行的最左侧边距。 你还可以选择该行并按 F9，选择“调试” > “切换断点”，或者右键单击并选择“断点” > “插入断点”    。 断点显示为代码行左边距中的一个红点。 调试器在行执行之前挂起执行。

![设置断点](../debugger/media/dbg_basics_setbreakpoint.png "设置断点")

Visual Studio 中的断点提供了一组丰富的附加功能，例如条件断点和跟踪点。 有关详细信息，请参阅[使用断点](../debugger/using-breakpoints.md)。

### <a name="run-to-a-function-breakpoint"></a>运行到函数断点

你可以让调试器一直运行，直到达到指定的函数。 可以通过名称指定函数，也可以从调用堆栈中选择函数。

**按名称指定函数断点**

1. 选择“调试” > “新建断点” > “函数断点”  

1. 在“新建函数断点”对话框中，键入函数名称并选择其语言。

   ![“新建函数断点”对话框](../debugger/media/dbg_execution_newbreakpoint.png "新建函数断点")

1. 选择“确定”。

如果函数已重载或位于多个命名空间中，则可以在“断点”窗口中选择所需的断点。

![重载函数断点](../debugger/media/dbg_execution_overloadedbreakpoints.png "重载函数断点")

**从调用堆栈中选择函数断点**

1. 调试时，通过选择“调试” > “窗口” > “调用堆栈”打开“调用堆栈”窗口。

1. 在“调用堆栈”窗口中，右键单击函数，然后选择“运行到光标处”，或按 Ctrl+F10 。

若要直观地跟踪调用堆栈，请参阅[调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

### <a name="run-to-a-cursor-location"></a>运行到光标位置

若要运行到光标位置，请在源代码或“调用堆栈”窗口中，选择要在其所在位置中断的行，右键单击并选择“运行到光标处”，或按 Ctrl +F10 。 选择“运行到光标处”和设置临时断点效果类似。

### <a name="run-to-click"></a>运行时单击

在调试器中暂停时，可将鼠标悬停在源代码中的某个语句上或“反汇编”窗口中，然后选择“将执行运行到此处”绿色箭头图标。 使用“运行到单击处”时，无需设置临时断点。

![运行到单击处](../debugger/media/dbg-run-to-click.png "运行时单击")

> [!NOTE]
> 从 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] 开始，“运行到单击处”可用。

### <a name="manually-break-into-code"></a>手动中断代码

若要在正在运行的应用中的下一可用代码行处中断，请选择“调试” > “全部中断”，或按 Ctrl+Alt+Break  。

## <a name="move-the-pointer-to-change-the-execution-flow"></a><a name="BKMK_Set_the_next_statement_to_execute"></a>移动指针以更改执行流

调试器暂停时，源代码或“反汇编”窗口空白处的黄色箭头标记要执行的下一条语句的位置。 你可以通过移动此箭头来更改要执行的下一条语句。 你可以跳过一部分代码，或者返回上一行。 在某些情况下移动指针很有用，例如，跳过包含已知 bug 的代码段。

 ![移动指针](../debugger/media/dbg_basics_example3.gif "移动指针")

若要更改要执行的下一条语句，调试器必须处于中断模式。 在源代码或“反汇编”窗口中，将黄色箭头拖动到另一行，或右键单击接下来要执行的行并选择“设置下一语句”。

程序计数器直接跳转到新位置，且新旧执行点之间的指令不会执行。 但是，如果后移执行点，则不撤销插入的指令。

>[!CAUTION]
>- 将下一条语句移动到另一个函数或范围通常会导致调用堆栈损坏，导致一个运行时错误或异常。 如果尝试将下一条语句移动到另一个范围，则调试器将打开一个含有警告的对话框，并提供一个取消该操作的机会。
>- 在 Visual Basic 中，不能将下一条语句移动到另一个范围或函数。
>- 在本机 C++ 中，如果已启用运行时检查，设置下一条语句会导致执行到达方法的结尾时引发异常。
>- 当启用“编辑并继续”时，如果你进行了“编辑并继续”无法立即重新映射的编辑，那么 **“设置下一语句”** 将失败。 例如，如果你编辑了 catch 块中的代码，将发生这种情况。 发生这种情况时，系统会显示一条错误消息，告诉你该操作不受支持。
>- 在托管代码中，如果出现以下情况，则不能移动下一条语句：
>   - 下一条语句与当前语句不在同一个方法中。
>   - 使用实时调试启动调试。
>   - 正在展开调用堆栈。
>   - 已引发一个 System.StackOverflowException 或 System.Threading.ThreadAbortException 异常。

## <a name="debug-non-user-code"></a><a name="BKMK_Restrict_stepping_to_Just_My_Code"></a>调试非用户代码

默认情况下，调试器会通过启用名为“仅我的代码”的设置来尝试仅调试你的应用代码。 有关此功能如何适用于不同项目类型和语言以及可以如何对其进行自定义的更多详细信息，请参阅[仅我的代码](../debugger/just-my-code.md)。

若要在调试时查看框架代码、第三方库代码或系统调用，可以禁用“仅我的代码”。 在“工具”（或“调试”）>“选项” > “调试”中，清除“启用仅我的代码”复选框。 如果禁用“仅我的代码”，非用户代码会在调试器窗口中显示，且调试器可以单步执行非用户代码。

> [!NOTE]
> 设备项目不支持“仅我的代码”。

### <a name="debug-system-code"></a>调试系统代码

如果你已加载 Microsoft 系统代码的调试符号，并已禁用“仅我的代码”，则可以单步执行系统调用，就像可以对其他任何调用所做的那样。

若要加载 Microsoft 符号，请参阅[配置符号位置和加载选项](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#configure-symbol-locations-and-loading-options)。

**加载特定系统组件的符号：**

1. 在调试时，通过选择“调试” > “窗口” > “模块”，或按 Ctrl+Alt+U   打开“模块”窗口。

1. 在“模块”窗口中，可以通过“符号状态”列了解哪些模块加载了符号。 右键单击要为其加载符号的模块，然后选择“加载符号”。

## <a name="step-into-properties-and-operators-in-managed-code"></a><a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a> 单步执行托管代码中的属性和运算符
 默认情况下，调试器将逐过程执行托管代码中的属性和运算符。 在多数情况下，这会提供较好的调试体验。 若要启用单步执行属性或运算符，请选择“调试” > “选项” 。 在“调试” > “常规”页面上，清除“逐过程执行属性和运算符(仅限托管)”复选框。

## <a name="see-also"></a>请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [初探调试](../debugger/debugger-feature-tour.md)
