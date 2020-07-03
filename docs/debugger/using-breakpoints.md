---
title: 在调试器中使用断点 |Microsoft Docs
ms.custom: ''
ms.date: 06/30/2020
ms.topic: how-to
f1_keywords:
- vs.debug.breakpointswin
- vs.debug.disassembly.insert
- vs.debug.sourcewin.edit
- vs.debug.file
- vs.debug.breakpt.new
- vs.debug.whenbreakpointishit
- vs.debug.breakpt.location.address
- vs.debug.breakpt.constraints
- vs.debug.breakpoints.delete
- vs.debug.breakpt.location.data
- vc.breakpoints
- vs.debug.breakpt.condition
- vs.debug.breakpt.location.function
- vs.debug.breakpoints
- vs.debug.menu.insert
- vs.debug.filenames
- vs.debug.breakpt.action
- vs.debug.sourcewin.insert
- vs.debug.address
- vs.debug.data
- vs.debug.func
- vs.debug.breakpt.location.file
helpviewer_keywords:
- breakpoints, about breakpoints
ms.assetid: 020b2e97-3b3e-4b2c-872d-b5c6025e120e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 57b2ea6a0c69387043057bc07957a757ed351f99
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769413"
---
# <a name="use-breakpoints-in-the-visual-studio-debugger"></a>在 Visual Studio 调试器中使用断点

在开发人员的工具箱中，断点是最重要的调试技术之一。 你可以在希望暂停调试器执行的任何位置设置断点。 例如，你可能想要查看代码变量的状态，或查看某个断点处的调用堆栈。  如果你正在尝试解决使用断点时出现的警告或问题，请参阅 [Visual Studio 调试器中的断点排除故障](../debugger/troubleshooting-breakpoints.md)。

> [!NOTE]
> 如果知道要解决的任务或问题，但想要了解应使用哪种断点，请参见[查找调试任务](../debugger/find-your-debugging-task.md#pause-running-code)。

## <a name="set-breakpoints-in-source-code"></a><a name="BKMK_Overview"></a> 在源代码中设置断点

可以在任意可执行代码行上设置断点。 例如，在下面的 C# 代码中，可以在包含变量声明 (`int testInt = 1`) 的代码行、`for` 循环或 `for` 循环内的任何代码上设置断点。 如果没有赋值和 getter/setter，则不能在方法签名、命名空间或类的声明，或者变量声明上设置断点。

若要在源代码中设置断点，请单击代码行最左边的边距。 你还可以选择行并按“F9”，选择“调试” > “切换断点”，或者右键单击并选择“断点” > “插入断点”    。 断点显示为左边距中的一个红点。

对于大多数语言（包括 C#），会自动突出显示断点和当前执行的行。 对于 C++ 代码，可以通过选择“工具”（或“调试”）>“选项” > “调试” >  “突出显示断点和当前语句的整个源行(仅限 C++)”    。

![设置断点](../debugger/media/basicbreakpoint.png "基本断点")

调试时，在执行断点所在行上的代码之前，执行会在断点处暂停。 断点符号显示黄色箭头。

在以下示例中的断点处，`testInt` 的值仍然为 1。 也就是说，从变量初始化（设置为值 1）以来，该值没有更改，因为尚未执行黄色的语句。

![断点执行已停止](../debugger/media/breakpointexecution.png "断点执行")

当调试器在断点处停止时，可以查看应用程序的当前状态，包括[变量值](../debugger/debugger-feature-tour.md#inspect-variables-with-data-tips)和[调用堆栈](../debugger/how-to-use-the-call-stack-window.md)。

下面是关于使用断点的一些常规说明。

- 断点是一个开关。 你可以单击它，按 F9，或使用“调试” > “切换断点”来删除或重新插入该断点  。

- 若要禁用断点而不删除它，请将鼠标悬停在其上或右键单击它，然后选择“禁用断点”。 禁用的断点在左边距或“断点”窗口中显示为空心圆点。 若要重新启用断点，请将鼠标悬停在断点上或右键单击它，然后选择“启用断点”。

- 设置条件和操作，添加和编辑标签，或通过右键单击断点并选择适当的命令导出断点，或将鼠标悬停在断点上并选择“设置”图标。

## <a name="breakpoint-actions-and-tracepoints"></a><a name="BKMK_Print_to_the_Output_window_with_tracepoints"></a>断点操作和跟踪点

“跟踪点”是将消息打印到“输出”窗口的断点。 跟踪点的作用像这种编程语言中的一个临时跟踪语句，且不会暂停代码的执行。 通过在“断点设置”窗口中设置特殊操作，可以创建跟踪点。 有关详细说明，请参阅[在 Visual Studio 调试器中使用跟踪点](../debugger/using-tracepoints.md)。

## <a name="breakpoint-conditions"></a>断点条件

可以通过设置条件来控制在何时何处执行断点。 条件可以是调试器能够识别的任何有效表达式。 有关有效表达式的详细信息，请参见[调试器中的表达式](../debugger/expressions-in-the-debugger.md)。

**设置断点条件：**

1. 右键单击该断点符号并选择“条件”。 或者将鼠标悬停在断点符号上，选择“设置”图标，然后在“断点设置”窗口中选择“条件”  。

   还可以在“断点”窗口中设置条件，方法是右键单击断点并选择“设置”，然后选择“条件”  。

   ![断点设置](../debugger/media/breakpointsettings.png "BreakpointSettings")

2. 在下拉列表中，选择“条件表达式”、“命中计数”或“筛选器”，并相应地设置其值  。

3. 选择“关闭”或按 Ctrl+Enter 关闭“断点设置”窗口   。 或者，从“断点”窗口中，选择“确定”以关闭对话框 。

设置了条件的断点在源代码和“断点”窗口中带有 + 符号 。

<a name="BKMK_Specify_a_breakpoint_condition_using_a_code_expression"></a>
### <a name="create-a-conditional-expression"></a>创建条件表达式

选择“条件表达式”时，可以在两个条件之间进行选择：“为 true”或“更改时” 。 要在满足表达式时中断，请选择“为 true”；要在表达式的值更改时中断，请选择“更改时” 。

在下面的示例中，仅当 `testInt` 的值为“4”时才会命中断点：

![断点条件为 true](../debugger/media/breakpointconditionistrue.png "断点为 true")

在下面的示例中，仅当 `testInt` 的值更改时才会命中断点：

![断点更改时](../debugger/media/breakpointwhenchanged.png "断点更改时")

如果使用无效语法设置断点条件，则会显示警告消息。 如果在指定断点条件时使用的语法有效但语义无效，则在第一次命中断点将出现警告消息。 在这两种情况下，调试器都会在遇到无效断点时中断。 仅在条件有效且计算结果为 `false`时才会跳过断点。

>[!NOTE]
>不同编程语言的“更改时”字段的行为不同。
>- 对于本机代码，调试器不会将条件的第一次计算当作一次更改，所以第一次计算时不会命中断点。
>- 对于托管代码，当选择了“更改时”，调试器将在之后的第一次计算时命中断点。

<a name="using-object-ids-in-breakpoint-conditions-c-and-f"></a>
### <a name="use-object-ids-in-conditional-expressions-c-and-f-only"></a>在条件表达式中使用对象 ID（仅限 C# 和 F#）

 有时，你想要观察特定对象的行为。 例如，你可能想要找出对象多次插入到集合中的原因。 在 C# 和 F# 中，可以创建[引用类型](/dotnet/csharp/language-reference/keywords/reference-types)的特定实例的对象 ID，并在断点条件下使用它们。 对象 ID 由公共语言运行时 (CLR) 调试服务生成并与该对象关联。

**创建对象 ID：**

1. 在创建对象后的代码中设置断点。

2. 开始调试，当执行在断点处暂停时，选择“调试” > “窗口” > “局部变量”或按 Alt+4 打开“局部变量”窗口     。

   在“局部变量”窗口中找到特定的对象实例，右键单击它，然后选择“生成对象 ID” 。

   应该会在“局部变量” **$** 窗口中看到 **$** 窗口中设置断点来中断调用函数返回到的指令或行处的执行。 这就是对象 ID。

3. 在想要开展调查时添加一个新断点，例如将对象添加到集合中时。 右键单击该断点并选择“条件”。

4. 在“条件表达式”字段中使用对象 ID。 例如，如果变量 `item` 是要添加到集合中的对象，则选择“为 true”，并键入“item == $\<n>”，其中 \<n> 是对象 ID 编号 。

   会在将该对象添加到集合中时中断执行。

   若要删除对象 ID，请右键单击“局部变量”窗口中的变量，然后选择“删除对象 ID” 。

> [!NOTE]
> 对象 ID 创建弱引用，且不会阻止对象被垃圾回收。 它们仅对当前调试会话有效。

### <a name="set-a-hit-count-condition"></a>设置命中次数条件

如果怀疑代码中的循环在一定数量的迭代后开始产生错误行为，则可以设置断点以在该次数的命中后停止执行，而不必反复按 F5 以到达该迭代。

在“断点设置”窗口的“条件”下，选择“命中计数”，然后指定迭代次数  。 在下面的示例中，将断点设置为每隔一次迭代命中一次：

![断点命中次数](../debugger/media/breakpointhitcount.png "BreakpointHitCount")

### <a name="set-a-filter-condition"></a>设置筛选条件

可以将断点限制为仅在指定设备上或在指定进程和线程中触发。

在“断点设置”窗口的“条件”下，选择“筛选器”，然后输入以下一个或多个表达式  ：

- MachineName = "name"
- ProcessId = value
- ProcessName = "name"
- ThreadId = value
- ThreadName = "name"

将字符串值放在双引号内。 可以使用 `&` (AND)、 `||` (OR)、 `!` (NOT) 和括号合并子句。

## <a name="set-function-breakpoints"></a><a name="BKMK_Set_a_breakpoint_in_a_source_file"></a> 设置函数断点

可以在调用函数时中断执行。 例如，当你知道函数名但不知道其位置时，这很有用。 如果多个函数（例如重载函数或不同项目中的函数）具有相同的名称，而你想要将其全部中断，这也很有用。

**设置函数断点：**

1. 选择“调试” > “新建断点” > “函数断点”，或按 Alt+F9 > Ctrl+B      。

   也可以在“断点”窗口中选择“新建” > “函数断点”  。

1. 在“新建函数断点”对话框中，在“函数名称”框中输入函数名称 。

   缩小函数规格：

   - 使用完全限定的函数名。

     示例：`Namespace1.ClassX.MethodA()`

   - 添加重载函数的参数类型。

     示例：`MethodA(int, string)`

   - 使用“!”符号指定模块。

     示例：`App1.dll!MethodA`

   - 使用本机 C++ 中的上下文运算符。

     `{function, , [module]} [+<line offset from start of method>]`

     示例：`{MethodA, , App1.dll}+2`

1. 在“语言”下拉列表中，选择函数的语言。

1. 选择“确定”。

### <a name="set-a-function-breakpoint-using-a-memory-address-native-c-only"></a>使用内存地址设置函数断点（仅限本机 C++）
 你还可以使用对象的地址在类的特定实例调用的方法上设置函数断点。  例如，给定一个类型为 `my_class` 的可寻址对象，可以在实例调用的 `my_method` 方法上设置函数断点。

1. 在实例化类的实例后的位置设置断点。

2. 找到实例的地址（例如 `0xcccccccc`）。

3. 选择“调试” > “新建断点” > “函数断点”，或按 Alt+F9 > Ctrl+B      。

4. 将下列内容添加到“函数名”框中，并选择“C++”语言 。

   ```cpp
   ((my_class *) 0xcccccccc)->my_method
   ```

::: moniker range=">= vs-2019"

## <a name="set-data-breakpoints-net-core-30-or-higher"></a><a name="BKMK_set_a_data_breakpoint_managed"></a>设置数据断点（.NET Core 3.0 或更高版本）

当特定对象的属性更改时，数据断点中断执行。

**设置数据断点**

1. 在 .NET Core 项目中，启动调试，并等待到达断点。

2. 在“自动”、“监视”或“局部变量”窗口中，右键单击一个属性并在上下文菜单中选择“当值更改时中断”   。

    ![托管数据断点](../debugger/media/managed-data-breakpoint.png "托管数据断点")

.NET Core 中的数据断点不适用于：

- 无法在工具提示、“局部变量”、“自动”或“监视”窗口中展开的属性
- 静态变量
- 具有 DebuggerTypeProxy 属性的类
- 结构内的字段

::: moniker-end

## <a name="set-data-breakpoints-native-c-only"></a><a name="BKMK_set_a_data_breakpoint_native_cplusplus"></a>设置数据断点（仅限本机 C++）

 数据断点在存储在指定内存地址中的值更改时中断执行。 如果只读取但不更改该值，则执行不会中断。

**设置数据断点：**

1. 在 C++ 项目中，启动调试，并等待到达断点。 在“调试”菜单上，选择“新建断点” > “数据断点”  

    还可以在“断点”窗口中选择“新建” > “数据断点”，或者右键单击“自动”、“监视”或“局部变量”窗口中的某个项，然后在上下文菜单中选择“当值更改时中断”      。

2. 在“地址”框中，键入内存地址或计算结果为内存地址的表达式。 例如，键入 `&avar` 以在变量 `avar` 的内容更改时执行中断操作。

3. 在 **“字节计数”** 下拉菜单中，选择你想要调试程序监视的字节数。 例如，如果选择 **4**，则调试程序将监视从 `&avar` 开始的四个字节，并在其中任何字节的值发生更改时执行中断操作。

数据断点在下列情况下无效：
- 将未经调试的进程写入内存位置。
- 在两个或多个进程间共享内存位置。
- 内存位置在内核内更新。 例如，如果内存传递给 32 位 Windows `ReadFile` 函数，则内存将从内核模式进行更新，因此调试器不会在更新时中断。
- 其中，监视表达式在 32 位硬件上大于 4 字节，在 64 位硬件上大于 8 字节。 这是 x86 体系结构的一个限制。

> [!NOTE]
> - 数据断点取决于特定的内存地址。 变量的地址随调试会话而更改，因此将在每个调试会话结束时自动禁用数据断点。
>
> - 如果在局部变量上设置数据断点，则断点在函数结束时仍处于启用状态，但内存地址不再适用，因此断点的行为不可预测。 如果在局部变量上设置了数据断点，则应在函数结束前删除或禁用该断点。

## <a name="manage-breakpoints-in-the-breakpoints-window"></a><a name="BKMK_Specify_advanced_properties_of_a_breakpoint_"></a>在“断点”窗口中管理断点

 可以使用“断点”窗口查看和管理解决方案中的所有断点。 在大型解决方案中，或者在断点非常重要的复杂调试方案中，这一集中位置尤为有用。

在“断点”窗口中，可以搜索、排列、筛选、启用/禁用或删除断点。 还可以设置条件和操作，或添加新的函数或数据断点。

若要打开“断点”窗口，请选择“调试” > “窗口” > “断点”，或按 Alt+F9 或 Ctrl+Alt      + B。

![“断点”窗口](../debugger/media/breakpointswindow.png "“断点”窗口")

若要选择要在“断点”窗口中显示的列，请选择“显示列” 。 选择列标题以按该列对断点列表进行排序。

### <a name="breakpoint-labels"></a><a name="BKMK_Set_a_breakpoint_at_a_function_return_in_the_Call_Stack_window"></a> 断点标签
可以使用标签对“断点”窗口中的断点列表进行排序和筛选。

1. 若要向断点添加标签，请在源代码或“断点”窗口中右键单击断点，然后选择“编辑标签” 。 添加新标签或选择现有标签，然后选择“确定”。
2. 通过选择“标签”、“条件”或其他列标题，在“断点”窗口中对断点列表进行排序  。 可以通过选择工具栏中的“显示列”来选择要显示的列。

### <a name="export-and-import-breakpoints"></a>导入和导出断点
 若要保存或共享断点的状态和位置，可以导出或导入断点。

- 若要将单个断点导出到 XML 文件，请在源代码或“断点”窗口中右键单击该断点，然后选择“导出”或“导出已选内容”  。 选择导出位置，然后选择“保存”。 默认位置是解决方案文件夹。
- 若要导出多个断点，请在“断点”窗口中选择断点旁边的框，或在“搜索”字段中输入搜索条件 。 选择“导出与当前搜索条件匹配的所有断点”图标，然后保存文件。
- 若要导出所有断点，请取消选中所有框并将“搜索”字段留空。 选择“导出与当前搜索条件匹配的所有断点”图标，然后保存文件。
- 若要导入断点，请在“断点”窗口中选择“从文件导入断点”图标，导航到 XML 文件位置，然后选择“打开”  。

## <a name="set-breakpoints-from-debugger-windows"></a><a name="BKMK_Set_a_breakpoint_from_debugger_windows"></a> 从调试器窗口设置断点

还可以从“调用堆栈”和“反汇编”调试器窗口设置断点 。

### <a name="set-a-breakpoint-in-the-call-stack-window"></a>在“调用堆栈”窗口中设置断点

 若要在调用函数返回的指令或行处中断，可以在“调用堆栈”窗口中设置断点。

**在调用堆栈窗口中设置断点：**

1. 若要打开“调用堆栈”窗口，必须在调试期间暂停。 选择“调试” > “窗口” > “调用堆栈”，或按 Ctrl+Alt+C     。

2. 在“调用堆栈”窗口中，右键单击调用函数并选择“断点” > “插入断点”，或按 F9   。

   断点符号显示在调用堆栈左边距中的函数调用名称旁。

调用堆栈断点在“断点”窗口中显示为一个地址，其内存位置对应于函数中的下一个可执行指令。

调试器在指令处中断。

有关调用堆栈的详细信息，请参阅[如何：使用“调用堆栈”窗口](../debugger/how-to-use-the-call-stack-window.md)。

要在代码执行期间以可视化方式跟踪断点，请参阅[调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

### <a name="set-a-breakpoint-in-the-disassembly-window"></a>在“反汇编”窗口中设置断点

1. 若要打开“反汇编”窗口，必须在调试期间暂停。 选择“调试” > “窗口” > “反汇编”，或按 Alt+8    。

2. 在“反汇编”窗口中，单击要中断的指令的左边距。 你还可以选择它并按 F9，或者右键单击并选择“断点” > “插入断点”  。

## <a name="see-also"></a>请参阅

- [什么是调试？](../debugger/what-is-debugging.md)
- [使用 Visual Studio 编写更好的 C# 代码](../debugger/write-better-code-with-visual-studio.md)
- [初探调试](../debugger/debugger-feature-tour.md)
- [Visual Studio 调试器中的断点排除故障](../debugger/troubleshooting-breakpoints.md)
