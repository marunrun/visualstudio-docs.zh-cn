---
title: 导航调试会话 (Xaml 和C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 1da33203-333f-4a05-b4e2-8d407c497233
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b5b8d24f01f7882e8c760918119a03a1c489c727
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156828"
---
# <a name="navigate-a-debugging-session-in-visual-studio-xaml-and-c"></a>在 Visual Studio 中导航调试会话（Xaml 和 C#）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本快速入门演示如何导航 Visual Studio 调试会话以及如何在会话中查看和更改程序状态。

 本快速入门适用于刚开始使用 Visual Studio 进行调试的开发人员以及要详细了解 Visual Studio 调试会话中的导航的开发人员。 它并不讲解调试本身的技巧。 示例代码中的方法仅用于演示本主题中所述的调试过程。 这些方法不使用应用或函数设计的最佳做法。 事实上，你很快就会发现这些方法（以及应用本身）完全没什么太多作用。

 本快速入门的各部分设计为尽可能独立，因此你可以跳过任何包含已熟悉的信息的部分。 你也无需创建示例应用；不过我们确实建议这样做，并且已尽可能简化了过程。

 **调试器键盘快捷方式。** Visual Studio 调试器导航同时针对鼠标和键盘进行了优化。 本主题中的许多步骤都在括号备注中包含键盘加速器或快捷键。 例如，(键盘：F5) 指示按 F5 键启动或继续调试器的执行。

## <a name="in-this-topic"></a>在本主题中
 你可以学习如何：

- [创建示例应用](#BKMK_CreateTheApplication)

- [设置和运行到断点、单步执行方法以及检查程序数据](#BKMK_StepInto)

- [单步执行、逐过程执行和跳出执行方法](#BKMK_StepIntoOverOut)

- [设置条件断点、运行到光标处以及可视化变量](#BKMK_ConditionCursorVisualize)

- [编辑并继续，从异常中恢复](#BKMK_EditContinueRecoverExceptions)

## <a name="BKMK_CreateTheApplication"></a> 创建示例应用
 调试与代码有关，因此示例应用仅使用 Windows 应用商店应用程序框架创建一个源文件，在该文件中可以查看调试会话导航的工作原理以及如何检查和更改程序状态。 将调用的所有代码都从主页的构造函数进行调用；不添加任何控件，并且不处理任何事件。

 **创建默认 C# Windows 应用商店应用。** 打开 Visual Studio。 在主页上，选择 **“新建项目”** 链接。 在“新建项目”对话框中，在 **“已安装”** 列表中选择 **“Visual C#”** ，然后选择 **“Windows 应用商店”** 。 在项目模板列表中，选择 **“应用程序”** 。 Visual Studio 随即创建一个新解决方案和项目，并显示 MainPage.xaml 设计器和 XAML 代码编辑器。

 **打开 MainPage.xaml.cs 源文件。** 右键单击 XML 编辑器中的任何位置，然后选择 **“查看代码”** 。 MainPage.xaml.cs 代码隐藏文件随即显示。 请注意，该文件中仅列出一个方法（即 `MainPage()` 构造函数）。

 **将 MainPage 构造函数替换为示例代码。** 删除 MainPage() 方法。 单击以下链接：[调试器导航示例代码 (Xaml 和C#)](../debugger/debugger-navigation-sample-code-xaml-and-csharp.md)，然后将复制中列出的代码C#部分到剪贴板。 (选择**回**在浏览器或帮助查看器以返回到本快速入门页。)在 Visual Studio 编辑器中，在 `partial class MainPage` 块中粘贴代码。 选择 Ctrl + s 以保存文件。

 现在可以遵循本主题中的示例进行操作。

## <a name="BKMK_StepInto"></a> 设置和运行到断点、单步执行方法以及检查程序数据
 您可以启动调试会话的最常见方法是选择**开始调试**从**调试**菜单 (键盘：F5）。 执行随即开始，并一直继续到达到断点、手动挂起执行、发生异常或应用结束。

 当在调试器中挂起执行时，可以通过将鼠标悬停在变量上方，在数据提示中查看活动变量的值。 还可以打开“局部变量”和“自动”窗口，以查看活动变量及其当前值的列表。 通过将一个或多个变量添加到监视窗口可以在应用继续执行时关注变量的值。

 挂起应用的执行（这也称为中断到调试器中）之后，可以控制其余程序代码的执行方式。 可以逐行继续执行（从一个方法调用移动到该方法本身），也可以单步执行调用的方法。 这些过程称为逐步执行应用。 还可以继续应用的标准执行，从而运行到设置的下一个断点，或运行到放置光标的行。 可以随时停止调试会话。 调试器设计为可执行必要的清理操作并退出执行。

### <a name="example-1"></a>示例 1
 在此示例中，你会在 MainPage.xaml.cs 文件的 MainPage 构造函数中设置断点，单步执行第一个方法，查看变量值，然后停止调试。

 **设置断点。** 在 MainPage 构造函数中的 `methodTrack = "Main Page";` 语句处设置断点。 选择源代码编辑器的阴影滚动条槽中的行 (键盘：将光标置于该行上并按 F9 键）。

 ![单步执行](../debugger/media/dbg-basics-stepinto.png "DBG_Basics_StepInto")

 该断点图标将显示在滚动条槽中。

 **运行到断点处。** 通过选择来启动调试会话**开始调试**上**调试**菜单 (键盘：F5）。

 应用随即开始执行，并恰好在设置了断点的语句前挂起执行。 滚动条槽中的当前行图标标识你的位置，当前语句会突出显示。

 ![设置断点](../debugger/media/dbg-basics-setbreakpoint.png "DBG_Basics_SetBreakpoint")

 你现在可控制应用的执行，并且可以在逐步执行程序语句时检查程序状态。

 **单步执行方法。** 上**调试**菜单中，选择**单步执行**(键盘：F11)。

 ![当前行](../debugger/media/dbg-basics-currentline.png "DBG_Basics_CurrentLine")

 请注意，调试器会移动到下一行，这是对 Example1 方法的调用。 再次选择“单步执行”。 调试器会移动到 Example1 方法的入口点。 这指示该方法已在调用堆栈上加载，并且用于本地变量的内存已分配。

 单步执行某个代码行时，调试器会执行以下操作之一：

- 如果下一个语句不是对解决方案中的函数的调用，则调试器会执行该语句，移动到下一个语句中，然后挂起执行。

- 如果下一个语句是对解决方案中的函数的调用，则调试器会移动到调用的函数的入口点，然后挂起执行。

  继续单步执行 Example1 的语句，直到达到退出点。 调试器会突出显示方法的右大括号。

  **在数据提示中查看变量值。** 将鼠标悬停在变量名上方时，变量的名称、值和类型会显示在数据提示中。

  ![调试器数据提示](../debugger/media/dbg-basics-datatip.png "DBG_Basics_DataTip")

  将鼠标悬停在变量 `a`上方。 记下名称、值和数据类型。 将鼠标悬停在变量 `methodTrack`上方。 记下名称、值和数据类型。

  **在“局部变量”窗口中检查变量值。** 在“新建项目” **“启动调试”** 菜单上指向 **“窗口”** ，然后选择 **“局部变量”** 。 （键盘：Alt+ 4)。

  ![局部变量窗口](../debugger/media/dbg-basics-localswindow.png "DBG_Basics_LocalsWindow")

  “局部变量”窗口是函数的参数和变量的树视图。 对象变量的属性是对象本身的子节点。 `this` 变量是每个对象方法中用于表示对象本身的隐藏参数。 在此例中，它表示 MainPage 类。 因为 `methodTrack` 是 MainPage 类的成员，所以其值和数据类型会在 `this`下方的行中列出。 展开 `this` 节点以查看 `methodTrack` 信息。

  **添加为 methodTrack 变量监视。** `methodWatch` 变量在本快速入门全篇中用于显示示例中调用的方法。 要更加方便地查看变量的值，请将它添加到监视窗口中。 在“局部变量”窗口中右键单击变量名，然后选择 **“添加监视”** 。

  ![监视窗口](../debugger/media/dbg-basics-watchwindow.png "DBG_Basics_WatchWindow")

  可以在监视窗口中监视多个变量。 只要挂起执行，便会更新受监视的变量的值（如“局部变量”窗口和数据提示窗口中的值）。 还可以从代码编辑器将变量添加到监视窗口中。 选择要监视的变量，右键单击，然后选择 **“添加监视”** 。

## <a name="BKMK_StepIntoOverOut"></a> 单步执行、逐过程执行和跳出执行方法
 与单步执行父方法调用的方法相反，逐过程执行方法会执行子方法，然后在父方法继续时在调用方法中挂起执行。 当你熟悉方法的工作方式，并且确定其执行不会影响正在调查的问题时，可以逐过程执行方法。

 逐过程执行不包含方法调用的代码行会如同单步执行该行一样执行该行。

 跳出子方法会继续执行方法，然后在方法返回其调用方法之后挂起执行。 当你确定长函数的其余部分不重要时，可以跳出该函数。

 逐过程执行和跳出执行函数都会执行函数。

 ![执行、 逐过程执行和跳出执行方法的步骤](../debugger/media/dbg-basics-stepintooverout.png "DBG_Basics_StepIntoOverOut")

### <a name="example-2"></a>示例 2
 在此示例中，你会单步执行、逐过程执行和跳出执行方法。

 **在 MainPage 构造函数中调用 Example2 方法。** 编辑 MainPage 构造函数，并将 `methodTrack = String.Empty;` 后的行替换为 `Example2();`。

 ![从 Demo 方法中调用 Example2](../debugger/media/dbg-basics-callexample2.png "DBG_Basics_CallExample2")

 **运行到断点处。** 通过选择来启动调试会话**开始调试**上**调试**菜单 (键盘：F5）。 调试器会在断点处挂起执行。

 **逐过程执行代码行。** 上**调试**菜单中，选择**单步跳过**(键盘：F10)。 调试器会按照与单步执行语句相同的方式来执行 `methodTrack = "MainPage";` 语句。

 **单步执行 Example2 和 Example2_A。** 按 F11 键，以单步执行 Example 2 方法。 继续单步执行 Example2 语句，直到达到行 `int x = Example2_A();`。 再次单步执行此行以移动到 Example2_A 的入口点。 继续单步执行 Example2_A 的每个语句，直到返回 Example2。

 ![Example2](../debugger/media/dbg-basics-example2.png "DBG_Basics_Example2")

 **逐过程执行函数。** 请注意，Example2 中的下一行 `int y = Example2_A();` 基本上与上一行相同。 可以安全地逐过程执行此行。 按 F10 键，以从 Example2 的恢复移动到对 Example2_A 的第二次调用。 按 F10 以逐过程执行此方法。 请注意， `methodTrack` 字符串指示两次执行了 Example2_A 方法。 你还会注意到，调试器会立即移动到下一行。 它不会在 Example2 的恢复点处挂起执行。

 **跳出函数。** 按 F11 键，以单步执行 Example2_B 方法。 请注意，Example2_B 与 Example2_A 没有太大不同。 若要跳出该方法，请选择**单步跳出**上**调试**菜单 (键盘：Shift + F11）。 请注意， `methodTrack` 变量指示执行了 Example2_B，并且调试器已返回 Example2 的恢复点。

 **停止调试。** 在调试菜单上选择停止调试 (键盘：Shift + F5)。 这会结束调试会话。

## <a name="BKMK_ConditionCursorVisualize"></a> 设置条件断点、运行到光标处以及可视化变量
 条件断点指定导致调试器挂起执行的条件。 条件通过可以计算为 true 或 false 的任何代码表达式进行指定。 例如，可以使用条件断点仅在某个变量达到特定值时才检查频繁调用的方法中的程序状态。

 运行到光标处如同设置一次性断点。 挂起执行时，可以在源代码中选择某行并继续执行，直到达到所选行。 例如，可以逐步执行方法中的循环并确定该循环中的代码是否正确执行。 可以运行到置于循环执行之后的光标，而不是逐步执行循环的每次迭代。

 有时，难以在数据提示或变量窗口的行中查看变量的值。 调试器可以在一个文本可视化工具中显示字符串、HTML 和 Xml，该工具在可滚动的窗口中提供值的格式化视图。

### <a name="example-3"></a>示例 3
 在此示例中，你会设置条件断点以循环的特定迭代处中断，然后运行到置于循环后的光标处。 还会在文本可视化工具中查看变量的值。

 **在 MainPage 构造函数中调用 Example3 方法。** 编辑 MainPage 构造函数，并将 `methodTrack = String.Empty;` 后的行替换为行 `Example3();`。

 ![从 Demo 方法中调用 Example3](../debugger/media/dbg-basics-callexample3.png "DBG_Basics_CallExample3")

 **运行到断点处。** 通过选择来启动调试会话**开始调试**上**调试**菜单 (键盘：F5）。 调试器会在 MainPage 方法中的断点处挂起执行。

 **单步执行 Example3 方法。** 选择**单步执行**上**调试**菜单 (键盘：F11) 若要将移动到 Example3 方法的入口点。 继续单步执行该方法，直到迭代了 `for` 块的一次或多次循环。 请注意，单步执行所有 1000 次迭代需要较长时间。

 **设置条件断点。** 在代码窗口的左滚动条槽中，右键单击行 `x += i;` ，然后选择 **“条件”** 。 选中 **“条件”** 复选框，然后在文本框中输入 `i == 500;` 。 选择 **“为 true”** 选项，然后选择 **“确定”** 。 通过断点可以检查 `for` 循环的第 500 次迭代处的值。

 ![断点条件对话框](../debugger/media/dbg-basics-breakpointcondition.png "DBG_Basics_BreakpointCondition")

 可以通过其白色十字来识别条件断点图标。

 ![条件断点](../debugger/media/dbg-basics-conditionalbreakpoint.png "DBG_Basics_ConditionalBreakpoint")

 **运行到断点处。** 在调试菜单上选择继续 (键盘：F5）。 在“局部变量”窗口中，确认 `i` 的当前值是否为 500。 请注意，变量 `s` 表示为单个行，比窗口长得多。

 **可视化字符串变量。** 单击 **的** “值” `s`。

 “文本可视化工具”窗口随即出现，字符串的值会显示为多行字符串。

 **运行到光标处。** 右键单击行`methodTrack += "->Example3";`，然后选择**运行到光标处**(键盘：将光标移动到行;Ctrl + F10）。 调试器会完成循环迭代，然后在该行处挂起执行。

 **停止调试。** 在调试菜单上选择停止调试 (键盘：Shift + F5)。 这会结束调试会话。

## <a name="BKMK_EditContinueRecoverExceptions"></a> 编辑并继续，从异常中恢复
 在某些情况下，当在 Visual Studio 调试器中中断到代码中时，你可以更改变量的值，甚至是语句的逻辑。 此功能称为编辑并继续。

 编辑并继续对于在异常处中断的情况特别有用。 可以“展开”执行以将执行移动到恰好位于发生异常之前的点，然后更改有问题的变量或语句并在不引发异常的状态中继续执行当前调试会话，而不是停止并重新启动调试所涉及的较长过程来避免异常。

 虽然可以在各种情况下使用编辑并继续功能，不过难以指定不支持编辑并继续功能的特定条件，因为条件取决于编程语言、程序堆栈的当前状态以及调试器能否在不会损坏进程的情况下更改状态。 确定是否支持某个编辑更改的最好办法就是进行尝试；通过调试器可以立即知道是否不支持该更改。

### <a name="example-4"></a>示例 4
 在此示例中，你会将调试器运行到异常，展开该异常，更正方法的逻辑，然后更改变量的值，以便可以继续执行方法。

 **在 MainPage 构造函数中调用 Example4 方法。** 编辑 MainPage() 构造函数，并将 `methodTrack = String.Empty;` 后的行替换为行 `Example4();`。

 ![从 Demo 方法中调用 Example4](../debugger/media/dbg-basics-callexample4.png "DBG_Basics_CallExample4")

 **运行到异常。** 通过选择来启动调试会话**开始调试**上**调试**菜单 (键盘：F5）。 再次按 F5 以继续执行。 调试器会在 Example4 方法中的异常处挂起执行，并显示异常对话框。

 ![异常对话框](../debugger/media/dbg-basics-exceptiondlg.png "DBG_Basics_ExceptionDlg")

 **更改程序逻辑。** 很明显，错误处于 `if` 条件中：当 `x` 等于 0 时，应更改 `x` 的值；当 `x` 不等于零不更改。 选择 **“中断”** 以修复方法的逻辑。 尝试编辑行时，另一个对话框会出现。

 ![编辑并继续对话框的](../debugger/media/dbg-basics-editandcontinuedlg.png "DBG_Basics_EditAndContinueDlg")

 选择 **“编辑”** ，然后将行 `if (x != 0)` 更改为 `if (x == 0)`。 调试器会将对程序逻辑的更改保存到源文件。

 **更改变量值。** 在数据提示中或“局部变量”窗口中检查 `x` 的值。 它仍然是 0（零）。 如果尝试执行导致原始异常的语句，则它仅仅再次引发。 可以更改 `x`的值。 在“局部变量”窗口中，双击 **x** 行的 **“值”** 列。 将值从 0 更改为 1。

 ![局部变量窗口中编辑值](../debugger/media/dbg-basics-editandcontinuefix.png "DBG_Basics_EditAndContinueFix")

 按 F11 键，以单步执行之前引发了异常的语句。 请注意，行会执行而不发生错误。 再次按 F11。

 **停止调试。** 上**调试**菜单中，选择**停止调试**(键盘：Shift + F5)。 这会结束调试会话。

## <a name="see-also"></a>请参阅
 [启动调试会话 (VB、 C#，C++和 XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) [触发器挂起、 继续和后台事件的 Windows 应用商店)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md) [在 Visual Studio 中调试应用](../debugger/debug-store-apps-in-visual-studio.md)
