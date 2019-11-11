---
title: 用调试器定位代码 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/12/2018
ms.topic: conceptual
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
ms.openlocfilehash: 6dfffdf0c12ea2a8f14769f26bb40a3943579248
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187590"
---
# <a name="navigate-through-code-with-the-visual-studio-debugger"></a>使用 Visual Studio 调试器在代码中导航

Visual Studio 调试器可帮助您在代码中导航，以检查应用程序的状态并显示其执行流。 你可以使用键盘快捷方式、调试命令、断点和其他功能快速访问你要检查的代码。 熟悉调试器导航命令和快捷方式可以更快、更轻松地查找和解决应用程序问题。  如果这是您第一次尝试调试代码，则在完成本文之前，您可能需要阅读[调试绝对](../debugger/debugging-absolute-beginners.md)和[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="get-into-break-mode"></a>进入 "中断模式"

在*中断模式*下，当函数、变量和对象保留在内存中时，将挂起应用程序执行。 调试器进入中断模式后，可以在代码中导航。 快速进入中断模式的最常见方法是：

- 按**F10**或**F11**开始代码单步执行。 这使你可以快速找到应用程序的入口点，然后你可以继续按步骤命令来导航代码。

- [运行到特定位置或函数](#BKMK_Break_into_code_by_using_breakpoints_or_Break_All)，例如，[设置断点](using-breakpoints.md)并启动应用。

   例如，在 Visual Studio 中的代码编辑器中，你可以使用 "**运行到光标处**" 命令启动应用程序、附加调试器并进入中断模式，然后按**F11**来导航代码。

   ![运行到光标处并单步执行代码](../debugger/media/navigate-code-code-stepping.gif "运行到光标处并单步执行代码")

进入中断模式后，可以使用各种命令在代码中导航。 处于中断模式时，可以检查变量的值以查找冲突或 bug。 对于某些项目类型，还可以在中断模式下对应用进行调整。

大多数调试器窗口（如 "**模块**" 和 "**监视**" 窗口）仅在调试器附加到应用时可用。 某些调试器功能（如在 "**局部变量**" 窗口中查看变量值或在 "**监视**" 窗口中计算表达式）仅在调试器暂停时才可用（即在中断模式下）。

> [!NOTE]
> 如果你中断了未加载源或符号（ *.pdb*）文件的代码，调试器将显示 "**未找到源文件**" 或 "**未找到符号**" 页，这些页可帮助你查找和加载文件。 请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 如果无法加载符号或源文件，你仍可以在 "**反汇编**" 窗口中调试程序集指令。

## <a name="step-through-code"></a>逐行执行代码

调试器步骤命令可帮助你检查应用状态，或了解有关其执行流程的详细信息。

### <a name="BKMK_Step_into__over__or_out_of_the_code"></a>逐行单步执行代码

若要在调试时在每个语句上停止，请使用**Debug** > **单步**执行，或按**F11**。

调试器逐句通过代码语句，而不是物理行。 例如，`if` 子句可以写在一行内：

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

但是，当单步执行此行时，调试器将该条件视为一步，将结果视为另一步。 在前面的示例中，条件为 true。

在嵌套函数调用上， **“逐语句”** 将进入并单步执行嵌套最深的函数。 例如，如果在 `Func1(Func2())` 上使用 "**单步**执行"，则调试器将单步执行函数 `Func2`。

>[!TIP]
>执行每行代码时，可以将鼠标悬停在变量上以查看其值，或者使用 "[局部变量](autos-and-locals-windows.md)" 和 "[监视](watch-and-quickwatch-windows.md)" 窗口来监视值的变化。 在单步执行函数时，还可以直观地跟踪[调用堆栈](how-to-use-the-call-stack-window.md)。 （仅适用于 Visual Studio Enterprise，请参阅[在调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)）。

### <a name="BKMK_Step_over_Step_out"></a>单步执行代码，并跳过一些函数

您可能不关心调试时的函数，或者您知道它的工作原理，如测试良好的库代码。 在代码单步执行时，可以使用以下命令跳过代码。 函数仍会执行，但调试器会跳过它们。

|键盘命令|调试菜单命令|描述|
|----------------------|------------------|-----------------|
|**F10**|**逐过程**|如果当前行包含函数调用，则 "**逐过程**" 将运行代码，然后在调用的函数返回后在代码的第一行处挂起执行。|
|Shift+F11|**跳出**|**单步**执行将继续运行代码，并在当前函数返回时挂起执行。 调试器将跳过当前函数。|

## <a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a>运行到特定位置或函数

当确切了解要检查的代码时，或者知道要开始调试的位置时，你可能更愿意直接运行到特定位置或函数。

### <a name="run-to-a-breakpoint-in-code"></a>在代码中运行到断点

若要在代码中设置简单断点，请单击要挂起执行的代码行旁边的最左边距。 还可以选择行并按**F9**，选择 "**调试**"  >  "**切换断点**"，或者右键单击并选择 "**断点**"  > **插入断点**"。 该断点在代码行旁边的左边距中显示为一个红点。 调试器将在行执行之前挂起执行。

![设置断点](../debugger/media/dbg_basics_setbreakpoint.png "设置断点")

Visual Studio 中的断点提供了一组丰富的附加功能，例如条件断点和跟踪点。 有关详细信息，请参阅[使用断点](../debugger/using-breakpoints.md)。

### <a name="run-to-a-function-breakpoint"></a>运行到函数断点

可以告知调试器运行，直到它到达指定的函数。 可以通过名称指定函数，也可以从调用堆栈中选择函数。

**按名称指定函数断点**

1. 选择**调试** > **新断点** > **函数断点**

1. 在 "**新建函数断点**" 对话框中，键入函数的名称并选择它的语言。

   !["新建函数断点" 对话框](../debugger/media/dbg_execution_newbreakpoint.png "新建函数断点")

1. 选择“确定”。

如果函数超载或在多个命名空间中，则可以在 "**断点**" 窗口中选择所需的一个。

![重载函数断点](../debugger/media/dbg_execution_overloadedbreakpoints.png "重载函数断点")

**从调用堆栈中选择函数断点**

1. 调试时，请通过选择 "**调试**"  > **Windows**  > **调用堆栈**"来打开"**调用堆栈**"窗口。

1. 在 "**调用堆栈**" 窗口中，右键单击函数并选择 "**运行到光标处**"，或按**Ctrl** +**F10**。

若要直观地跟踪调用堆栈，请参阅[调试时在调用堆栈上映射方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

### <a name="run-to-a-cursor-location"></a>运行到光标位置

若要运行到光标位置，请在源代码或 "**调用堆栈**" 窗口中，选择要在其处中断的行，右键单击并选择 "**运行到光标**处"，或按**Ctrl** +**F10**。 选择 "**运行到光标处**" 类似于设置临时断点。

### <a name="run-to-click"></a>运行时单击

在调试器中暂停时，可以将鼠标悬停在源代码或 "**反汇编**" 窗口中的语句上，并选择 "在**此处运行执行到此处**" 绿色箭头图标。 使用 **"运行" 单击**此无需设置临时断点。

![运行到单击处](../debugger/media/dbg-run-to-click.png "运行时单击")

> [!NOTE]
> 从 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]开始**运行到单击**。

### <a name="manually-break-into-code"></a>手动中断代码

若要在正在运行的应用程序中的下一个可用代码行内中断，请选择 "**调试**"  > **全部中断**"，或按**Ctrl** +**Alt** +**中断**。

## <a name="BKMK_Set_the_next_statement_to_execute"></a>移动指针以更改执行流

调试器暂停时，源代码或**反汇编**窗口边距中的黄色箭头标记要执行的下一条语句的位置。 通过移动此箭头，可以更改要执行的下一条语句。 可以跳过部分代码，或返回到上一行。 在跳过包含已知 bug 的代码段的情况下，移动指针非常有用。

 ![移动指针](../debugger/media/dbg_basics_example3.gif "移动指针")

若要更改下一个要执行的语句，调试器必须处于中断模式。 在源代码或 "**反汇编**" 窗口中，将黄色箭头拖到其他线条上，或右键单击想要执行的行，然后选择 "**设置下一语句**"。

程序计数器会直接跳转到新位置，而不会执行新旧执行点之间的指令。 但是，如果向后移动执行点，则不会撤消干预说明。

>[!CAUTION]
>- 将下一条语句移动到另一个函数或范围通常会导致调用堆栈损坏，导致一个运行时错误或异常。 如果尝试将下一条语句移动到另一个范围，则调试器将打开一个含有警告的对话框，并提供一个取消该操作的机会。
>- 在 Visual Basic 中，不能将下一条语句移动到另一个范围或函数。
>- 在本机 C++ 中，如果已启用运行时检查，设置下一条语句会导致执行到达方法的结尾时引发异常。
>- 当启用“编辑并继续”时，如果你进行了“编辑并继续”无法立即重新映射的编辑，那么 **“设置下一语句”** 将失败。 例如，如果你编辑了 catch 块中的代码，将发生这种情况。 发生这种情况时，将显示一条错误消息，指出不支持该操作。
>- 在托管代码中，在以下情况下不能移动下一条语句：
>   - 下一条语句与当前语句不在同一个方法中。
>   - 调试是通过实时调试开始的。
>   - 正在展开调用堆栈。
>   - 已引发一个 System.StackOverflowException 或 System.Threading.ThreadAbortException 异常。

## <a name="BKMK_Restrict_stepping_to_Just_My_Code"></a>调试非用户代码

默认情况下，调试程序将尝试通过启用名为*仅我的代码*的设置来仅调试你的应用程序代码。 有关此功能如何适用于不同的项目类型和语言的详细信息，以及如何对其进行自定义的详细信息，请参阅[仅我的代码](../debugger/just-my-code.md)。

若要在调试时查看框架代码、第三方库代码或系统调用，可以禁用仅我的代码。 在 "**工具**" （或 "**调试**"） >**选项**" > **调试**中，清除"**启用仅我的代码**"复选框。 如果禁用仅我的代码，则调试器窗口中将显示非用户代码，并且调试器可以单步执行非用户代码。

> [!NOTE]
> 设备项目不支持“仅我的代码”。

### <a name="debug-system-code"></a>调试系统代码

如果已为 Microsoft 系统代码加载了调试符号，并已禁用仅我的代码，则可以单步执行系统调用，就像对任何其他调用一样。

若要加载 Microsoft 符号，请参阅[配置符号位置和加载选项](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#configure-symbol-locations-and-loading-options)。

**加载特定系统组件的符号：**

1. 进行调试时，请通过选择 "**调试**"  > **Windows**  > **模块**，或按**Ctrl** +**Alt** +**U**打开 "**模块**" 窗口。

1. 在 "**模块**" 窗口中，可以判断哪些模块在 "**符号状态**" 列中加载了符号。 右键单击要为其加载符号的模块，然后选择 "**加载符号**"。

## <a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a> 单步执行托管代码中的属性和运算符
 默认情况下，调试器将逐过程执行托管代码中的属性和运算符。 在多数情况下，这会提供较好的调试体验。 若要启用单步执行属性或运算符，请选择 "**调试**"  > **选项**。 在“调试” > “常规”页面上，清除“逐过程执行属性和运算符(仅限托管)”复选框。

## <a name="see-also"></a>请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [首先查看调试](../debugger/debugger-feature-tour.md)
