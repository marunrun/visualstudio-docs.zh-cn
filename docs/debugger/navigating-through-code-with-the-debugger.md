---
title: 使用调试器导航代码 |微软文档
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
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301091"
---
# <a name="navigate-through-code-with-the-visual-studio-debugger"></a>使用可视化工作室调试器浏览代码

Visual Studio 调试器可以帮助您浏览代码以检查应用的状态并显示其执行流。 您可以使用键盘快捷键、调试命令、断点和其他功能快速访问要检查的代码。 熟悉调试器导航命令和快捷方式，可以更快、更轻松地查找和解决应用问题。  如果这是您第一次尝试调试代码，则可能需要在阅读本文之前阅读[绝对初学者](../debugger/debugging-absolute-beginners.md)调试以及[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="get-into-break-mode"></a>进入"中断模式"

在*中断模式下*，当函数、变量和对象保留在内存中时，应用执行将挂起。 调试器处于中断模式后，即可浏览代码。 快速进入中断模式的最常见方式是：

- 通过按**F10**或**F11**开始代码步进。 这允许您快速查找应用的入口点，然后可以继续按步骤命令来导航代码。

- [运行到特定位置或函数](#BKMK_Break_into_code_by_using_breakpoints_or_Break_All)，例如，通过[设置断点](using-breakpoints.md)并启动应用。

   例如，从 Visual Studio 中的代码编辑器中，可以使用 **"运行到游标"** 命令启动应用、附加调试器并进入中断模式，然后**F11**来导航代码。

   ![运行到光标并踏入代码](../debugger/media/navigate-code-code-stepping.gif "运行到光标并踏入代码")

进入中断模式后，可以使用各种命令浏览代码。 在中断模式下，可以检查变量的值以查找冲突或 Bug。 对于某些项目类型，您还可以在中断模式下对应用进行调整。

大多数调试器窗口（如 **"模块**"和 **"监视"** 窗口）仅在调试器附加到应用时才可用。 某些调试器功能（如在 **"局部变量"** 窗口中查看变量值或"**监视"** 窗口中的评估表达式）仅在调试器暂停时（即处于中断模式）可用。

> [!NOTE]
> 如果闯入的代码没有加载源或符号 *（.pdb*） 文件，调试器将显示 **"未找到的源文件**"或 **"未找到符号"** 页面，以帮助您查找和加载这些文件。 请参阅[指定符号 （.pdb） 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 如果无法加载符号或源文件，仍可以在 **"拆解"** 窗口中调试程序集指令。

## <a name="step-through-code"></a>逐行执行代码

调试器步骤命令可帮助您检查应用状态或了解有关其执行流的更多信息。

### <a name="step-into-code-line-by-line"></a><a name="BKMK_Step_into__over__or_out_of_the_code"></a>逐行执行代码

要在调试时停止每个语句，请使用**调试** > **步骤输入**， 或按**F11**。

调试器通过代码语句，而不是物理行。 例如，`if` 子句可以写在一行内：

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

但是，当您踏入此行时，调试器将条件视为一个步骤，并将结果视为另一个步骤。 在前面的示例中，条件为 true。

在嵌套函数调用上， **“逐语句”** 将进入并单步执行嵌套最深的函数。 例如，如果在调用（如`Func1(Func2())`）上使用 **"步进**"，则调试器将踏`Func2`入函数。

>[!TIP]
>执行每行代码时，可以将鼠标悬停在变量上以查看其值，或使用["局部变量](autos-and-locals-windows.md)"和["监视"](watch-and-quickwatch-windows.md)窗口监视值更改。 您还可以在步进函数时直观地跟踪[调用堆栈](how-to-use-the-call-stack-window.md)。 （仅适用于可视化工作室企业版，请参阅[调试时调用堆栈上的映射方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

### <a name="step-through-code-and-skip-some-functions"></a><a name="BKMK_Step_over_Step_out"></a>单步执行代码并跳过一些函数

调试时可能不关心函数，或者知道它有效，就像经过良好测试的库代码一样。 在代码执行期间，可以使用以下命令跳过代码。 函数仍在执行，但调试器跳过它们。

|键盘命令|调试菜单命令|说明|
|----------------------|------------------|-----------------|
|**F10**|**单步执行**|如果当前行包含函数调用，**则"单步执行**"将运行代码，然后在被调用的函数返回后在第一行代码暂停执行。|
|**换档**+**F11**|**走出来**|**"退出"** 将继续运行代码，并在当前函数返回时暂停执行。 调试器跳过当前函数。|

## <a name="run-to-a-specific-location-or-function"></a><a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a>运行到特定位置或功能

当您确切知道要检查的代码或知道要从何处开始调试时，您可能更喜欢直接运行到特定位置或函数。

### <a name="run-to-a-breakpoint-in-code"></a>运行到代码中的断点

要在代码中设置一个简单的断点，请单击要挂起执行的代码行旁边的最左边边距。 您还可以选择线并按**F9，** 选择 **"调试** > **切换断点**"，或右键单击并选择**断点** > **插入断点**。 断点在代码行旁边的左边距显示为红点。 调试器在行执行之前暂停执行。

![设置断点](../debugger/media/dbg_basics_setbreakpoint.png "设置断点")

Visual Studio 中的断点提供了一组丰富的附加功能，例如条件断点和跟踪点。 有关详细信息，请参阅[使用断点](../debugger/using-breakpoints.md)。

### <a name="run-to-a-function-breakpoint"></a>运行到函数断点

您可以告诉调试器运行，直到它到达指定的函数。 可以通过名称指定函数，也可以从调用堆栈中选择函数。

**按名称指定函数断点**

1. 选择**调试** > **新断点** > **函数断点**

1. 在 **"新建函数断点"** 对话框中，键入函数的名称并选择其语言。

   ![新增功能断点对话框](../debugger/media/dbg_execution_newbreakpoint.png "新功能断点")

1. 选择“确定”。

如果函数过载或有多个命名空间，则可以在 **"断点"** 窗口中选择所需的函数。

![重载功能断点](../debugger/media/dbg_execution_overloadedbreakpoints.png "重载功能断点")

**从调用堆栈中选择函数断点**

1. 调试时，通过选择 **"调试** > **Windows** > **调用堆栈**"打开**调用堆栈**窗口。

1. 在 **"调用堆栈"** 窗口中，右键单击函数并**选择"运行到光标**"，或按**Ctrl**+**F10**。

要直观地跟踪调用堆栈，请参阅[调试时调用堆栈上的 Map 方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

### <a name="run-to-a-cursor-location"></a>运行到光标位置

要运行到游标位置，请在源代码或**调用堆栈**窗口中选择要中断的行，右键单击并选择"**运行到光标**"，或按**Ctrl**+**F10**。 选择 **"运行到游标"** 类似于设置临时断点。

### <a name="run-to-click"></a>运行时单击

在调试器中暂停时，可以将鼠标悬停在源代码或 **"拆解"** 窗口中的语句上，然后选择"**运行执行"到此处**的绿色箭头图标。 使用 **"运行"单击**无需设置临时断点。

![运行以单击](../debugger/media/dbg-run-to-click.png "运行时单击")

> [!NOTE]
> **运行到单击**可从 中[!include[vs_dev15](../misc/includes/vs_dev15_md.md)]开始。

### <a name="manually-break-into-code"></a>手动中断代码

要在正在运行的应用中断开下一行可用代码，请选择 **"全部调试** > **中断**"，或按**Ctrl**+**Alt**+**中断**。

## <a name="move-the-pointer-to-change-the-execution-flow"></a><a name="BKMK_Set_the_next_statement_to_execute"></a>移动指针以更改执行流

当调试器暂停时，源代码或**拆解**窗口的边距中黄色箭头标记要执行的下一个语句的位置。 您可以通过移动此箭头更改要执行的下一个语句。 您可以跳过部分代码，或返回到上一行。 移动指针对于跳过包含已知 Bug 的代码部分等情况非常有用。

 ![移动指针](../debugger/media/dbg_basics_example3.gif "移动指针")

要更改要执行的下一个语句，调试器必须处于中断模式。 在源代码或**拆解**窗口中，将黄色箭头拖动到其他行，或右键单击要执行的下一行，然后选择"**设置下一个语句**"。

程序计数器直接跳转到新位置，并且不会执行新旧执行点之间的指令。 但是，如果向后移动执行点，则中间指令不会撤消。

>[!CAUTION]
>- 将下一条语句移动到另一个函数或范围通常会导致调用堆栈损坏，导致一个运行时错误或异常。 如果尝试将下一条语句移动到另一个范围，则调试器将打开一个含有警告的对话框，并提供一个取消该操作的机会。
>- 在 Visual Basic 中，不能将下一条语句移动到另一个范围或函数。
>- 在本机 C++ 中，如果已启用运行时检查，设置下一条语句会导致执行到达方法的结尾时引发异常。
>- 当启用“编辑并继续”时，如果你进行了“编辑并继续”无法立即重新映射的编辑，那么 **“设置下一语句”** 将失败。 例如，如果你编辑了 catch 块中的代码，将发生这种情况。 发生这种情况时，一条错误消息告诉您不支持该操作。
>- 在托管代码中，如果以下情况：则无法移动下一个语句：
>   - 下一条语句与当前语句不在同一个方法中。
>   - 调试由实时调试启动。
>   - 呼叫堆栈展开正在进行中。
>   - 已引发一个 System.StackOverflowException 或 System.Threading.ThreadAbortException 异常。

## <a name="debug-non-user-code"></a><a name="BKMK_Restrict_stepping_to_Just_My_Code"></a>调试非用户代码

默认情况下，调试器尝试通过启用名为 *"仅我的代码"* 的设置来仅调试应用代码。 有关此功能如何适用于不同的项目类型和语言以及如何自定义它的详细信息，请参阅["我的代码](../debugger/just-my-code.md)"。

要查看调试时的框架代码、第三方库代码或系统调用，可以禁用"仅我的代码"。 在 **"工具**（或**调试**）>**选项** > **调试**中，清除"**仅启用我的代码"** 复选框。 禁用"仅我的代码"时，调试器窗口中将显示非用户代码，调试器可以单步进入非用户代码。

> [!NOTE]
> 设备项目不支持“仅我的代码”。

### <a name="debug-system-code"></a>调试系统代码

如果已加载了 Microsoft 系统代码的调试符号，并禁用了"仅我的代码"，则可以像任何其他调用一样进入系统调用。

要加载 Microsoft 符号，请参阅[配置符号位置和加载选项](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#configure-symbol-locations-and-loading-options)。

**要加载特定系统组件的符号，**

1. 调试时，通过选择**调试** > **Windows** > **模块**或按**Ctrl**+**Alt**+**U**打开 **"模块"** 窗口。

1. 在 **"模块"** 窗口中，您可以分辨哪些模块在 **"符号状态"** 列中加载了符号。 右键单击要为其加载符号的模块，然后选择 **"加载符号**"。

## <a name="step-into-properties-and-operators-in-managed-code"></a><a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a>在托管代码中逐步进入属性和运算符
 默认情况下，调试器将逐过程执行托管代码中的属性和运算符。 在多数情况下，这会提供较好的调试体验。 要启用单步执行到属性或运算符，请选择**调试** > **选项**。 在 **"调试** > **常规"** 页上，清除 **"对属性和运算符（仅限托管）"复选框**。

## <a name="see-also"></a>另请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [首先查看调试](../debugger/debugger-feature-tour.md)
