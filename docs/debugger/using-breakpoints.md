---
title: 在调试器中使用断点 |微软文档
ms.custom: ''
ms.date: 10/28/2019
ms.topic: conceptual
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
ms.openlocfilehash: a6a8ee96834fc20186ba6719a7c4f377fea45d6b
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301025"
---
# <a name="use-breakpoints-in-the-visual-studio-debugger"></a>在可视化工作室调试器中使用断点

断点是开发人员工具箱中最重要的调试技术之一。 无论要暂停调试器执行的任何位置，都可以设置断点。 例如，您可能希望查看代码变量的状态，或查看某个断点处的调用堆栈。  如果在使用断点时尝试解决警告或问题，请参阅[Visual Studio 调试器中的"故障排除断点](../debugger/troubleshooting-breakpoints.md)"。

> [!NOTE]
> 如果您知道要解决的任务或问题，但需要知道要使用的断点类型，请参阅[查找调试任务](../debugger/find-your-debugging-task.md#pause-running-code)。

## <a name="set-breakpoints-in-source-code"></a><a name="BKMK_Overview"></a>在源代码中设置断点

可以在任意可执行代码行上设置断点。 例如，在以下 C# 代码中，可以在变量声明、`for`循环或循环中的任何代码上`for`设置断点。 不能在命名空间或类声明或方法签名上设置断点。

要设置源代码中的断点，请单击代码行旁边的最左边边距。 您还可以选择线并按**F9，** 选择**调试** > **切换断点**，或右键单击并选择**断点** > **插入断点**。 断点在左边距显示为红点。

对于大多数语言（包括 C#），断点和当前执行行会自动突出显示。 对于C++代码，您可以通过选择 **"工具**（或**调试**）>**选项** > **调试** >  **突出显示断点和当前语句（仅限C++）的整个源行**来打开断点和当前行的突出显示。

![设置断点](../debugger/media/basicbreakpoint.png "基本断点")

调试时，在执行该行上的代码之前，执行会在断点处暂停。 断点符号显示黄色箭头。

在下面的示例中的断点处，值`testInt`仍为 1。 因此，自变量初始化（设置为值 1）以来，该值一直未更改，因为黄色语句尚未执行。

![断点执行已停止](../debugger/media/breakpointexecution.png "断点执行")

当调试器停止在断点时，可以查看应用的当前状态，包括[变量值](../debugger/debugger-feature-tour.md#inspect-variables-with-data-tips)和[调用堆栈](../debugger/how-to-use-the-call-stack-window.md)。

以下是有关使用断点的几条常规说明。

- 断点是切换。 您可以单击它，按**F9**，或使用**调试** > **切换断点**删除或重新插入它。

- 要禁用断点而不删除它，请悬停在断点上或右键单击它，然后选择"**禁用断点**"。 禁用的断点在左边距或**断点**窗口中显示为空点。 要重新启用断点，请悬停在断点上或右键单击它，然后选择"**启用断点**"。

- 设置条件和操作、添加和编辑标签，或通过右键单击并选择适当的命令导出断点，或将鼠标悬停在它上并选择 **"设置"** 图标。

## <a name="breakpoint-actions-and-tracepoints"></a><a name="BKMK_Print_to_the_Output_window_with_tracepoints"></a>断点操作和跟踪点

“跟踪点”是将消息打印到“输出”窗口的断点******。 跟踪点可以充当编程语言中的临时跟踪语句，并且不会暂停代码的执行。 通过在 **"断点设置"** 窗口中设置特殊操作来创建跟踪点。 有关详细说明，请参阅[在可视化工作室调试器中使用跟踪点](../debugger/using-tracepoints.md)。

## <a name="breakpoint-conditions"></a>断点条件

可以通过设置条件来控制在何时何处执行断点。 条件可以是调试器识别的任何有效表达式。 有关有效表达式的详细信息，请参阅[调试器 中的表达式](../debugger/expressions-in-the-debugger.md)。

**要设置断点条件：**

1. 右键单击断点符号并选择 **"条件**"。 或将鼠标悬停在断点符号上，选择 **"设置"** 图标，然后在 **"断点设置"** 窗口中选择 **"条件**"。

   您还可以通过右键单击断点并选择 **"设置**"，然后选择"条件"，在 **"断点**"窗口中设置**条件**。

   ![“断点设置”](../debugger/media/breakpointsettings.png "断点设置")

2. 在下拉列表中，选择**条件表达式**、**命中计数**或**筛选器**，并相应地设置该值。

3. 选择 **"关闭**"或按 **"Ctrl**+**Enter"** 以关闭**断点设置**窗口。 或者，从 **"断点"** 窗口中选择 **"确定"** 以关闭对话框。

设置条件的突破点在源代码和**+****断点**窗口中带有符号。

<a name="BKMK_Specify_a_breakpoint_condition_using_a_code_expression"></a>
### <a name="create-a-conditional-expression"></a>创建条件表达式

选择**条件表达式**时，可以在两个条件之间进行选择：**为 true**或**更改时**。 选择 true 在满足表达式时中断，或**当表达式**的值发生更改时更改为中断时更改为 **"true"。**

在下面的示例中，仅当 值`testInt`为**4**时才会命中断点：

![断点条件为 true](../debugger/media/breakpointconditionistrue.png "断点为真")

在下面的示例中，仅当`testInt`更改的值时才会命中断点：

![断点更改时](../debugger/media/breakpointwhenchanged.png "断点更改时")

如果使用无效语法设置断点条件，则会显示警告消息。 如果在指定断点条件时使用的语法有效但语义无效，则在第一次命中断点将出现警告消息。 在这两种情况下，调试器在达到无效的断点时会中断。 仅在条件有效且计算结果为 `false`时才会跳过断点。

>[!NOTE]
>对于不同的编程语言，"**更改时"** 字段的行为是不同的。
>- 对于本机代码，调试器并不认为对条件的第一次评估是更改，因此不会在第一次评估时触及断点。
>- 对于托管代码，调试器在选择**更改后**的第一次评估中命中断点。

<a name="using-object-ids-in-breakpoint-conditions-c-and-f"></a>
### <a name="use-object-ids-in-conditional-expressions-c-and-f-only"></a>在条件表达式中使用对象指示（仅限 C# 和 F#）

 有时，您希望观察特定对象的行为。 例如，您可能希望找出对象多次插入到集合中的原因。 在 C# 和 F# 中，可以为[引用类型](/dotnet/csharp/language-reference/keywords/reference-types)的特定实例创建对象 I，并在断点条件中使用它们。 对象 ID 由公共语言运行时 (CLR) 调试服务生成并与该对象关联。

**要创建对象 ID，**

1. 在创建对象后，在代码中的某个位置设置断点。

2. 开始调试，当执行在断点暂停时，选择 **"调试** > **Windows** > **局部变量**"或 **"Alt**+**4"** 以打开 **"局部变量"** 窗口。

   在 **"局部变量"** 窗口中查找特定对象实例，右键单击它，然后选择 **"使对象 ID**"。

   您应该在**$****"局部变量"** 窗口中看到加号。 这就是对象 ID。

3. 在要调查的点添加新的断点;例如，当要将对象添加到集合时。 右键单击该断点并选择“条件”****。

4. 在“条件表达式”字段中使用对象 ID****。 `item`例如，如果变量是要添加到集合的对象，请选择 **"为 true"，** 然后键入项 **= $\<n>，** 其中\<n>是对象 ID 号。

   会在将该对象添加到集合中时中断执行。

   要删除对象 ID，请右键单击 **"局部变量"** 窗口中的变量，然后选择 **"删除对象 ID**"。

> [!NOTE]
> 对象 ID 创建弱引用，且不会阻止对象被垃圾回收。 它们仅对当前调试会话有效。

### <a name="set-a-hit-count-condition"></a>设置命中计数条件

如果您怀疑代码中的循环在一定数量的迭代后开始行为不端，则可以设置断点以在该命中数后停止执行，而不必重复按**F5**才能达到该迭代。

在 **"断点设置"** 窗口中**的条件**下，选择 **"命中计数**"，然后指定迭代次数。 在下面的示例中，断点设置为在所有其他迭代中命中：

![断点命中计数](../debugger/media/breakpointhitcount.png "断点HitCount")

### <a name="set-a-filter-condition"></a>设置筛选器条件

可以将断点限制为仅在指定设备上或在指定进程和线程中触发。

在 **"断点设置"** 窗口中**的条件**下，选择 **"筛选**"，然后输入以下一个或多个表达式：

- MachineName = "name"
- ProcessId = value
- ProcessName = "name"
- ThreadId = value
- ThreadName = "name"

将字符串值放在双引号内。 可以使用 `&` (AND)、 `||` (OR)、 `!` (NOT) 和括号合并子句。

## <a name="set-function-breakpoints"></a><a name="BKMK_Set_a_breakpoint_in_a_source_file"></a>设置功能断点

在调用函数时，可以中断执行。 例如，当您知道函数名称但不知道它的位置时，这非常有用。 如果您具有同名函数，并且想要断开所有函数（如不同项目中的重载函数或函数），则它还很有用。

**要设置函数断点：**

1. 选择 **"调试** > **新断点** > **"功能断点**，或按**Alt**+**F9** > **Ctrl**+**B**。

   您还可以在 **"断点"** 窗口中选择 **"新功能** > **断点**"。

1. 在 **"新功能断点"** 对话框中，在 **"函数名称"框中输入函数名称**。

   要缩小功能规范：

   - 使用完全限定的函数名称。

     示例：`Namespace1.ClassX.MethodA()`

   - 添加重载函数的参数类型。

     示例：`MethodA(int, string)`

   - 使用"！"符号指定模块。

     示例： `App1.dll!MethodA`

   - 在本机C++中使用上下文运算符。

     `{function, , [module]} [+<line offset from start of method>]`

     示例： `{MethodA, , App1.dll}+2`

1. 在 **"语言**"下拉列表中，选择函数的语言。

1. 选择“确定”。

### <a name="set-a-function-breakpoint-using-a-memory-address-native-c-only"></a>使用内存地址设置函数断点（仅限本机C++）
 可以使用对象的地址在类的特定实例调用的方法上设置函数断点。  例如，给定类型`my_class`的对象，可以在实例调用`my_method`的方法上设置函数断点。

1. 在实例实例实例实例实例实例实例实例实例后，在某处设置断点。

2. 查找实例的地址（例如， `0xcccccccc`

3. 选择 **"调试** > **新断点** > **"功能断点**，或按**Alt**+**F9** > **Ctrl**+**B**。

4. 将以下内容添加到 **"功能名称**"框中，然后选择**C++** 语言。

   ```cpp
   ((my_class *) 0xcccccccc)->my_method
   ```

::: moniker range=">= vs-2019"

## <a name="set-data-breakpoints-net-core-30-or-higher"></a><a name="BKMK_set_a_data_breakpoint_managed"></a>设置数据断点（.NET Core 3.0 或更高）

当特定对象的属性发生更改时，数据断点会中断执行。

**设置数据断点**

1. 在 .NET Core 项目中，开始调试，然后等待到达断点。

2. 在 **"自动**"、"**监视**"或 **"局部变量"** 窗口中，右键单击属性，并在上下文菜单中**的值更改时选择"中断**"。

    ![托管数据断点](../debugger/media/managed-data-breakpoint.png "托管数据断点")

.NET Core 中的数据断点不适合：

- 工具提示、局部变量、自动或监视窗口中不可扩展的属性
- 静态变量
- 具有调试器TypeProxy属性的类
- 结构内的字段

::: moniker-end

## <a name="set-data-breakpoints-native-c-only"></a><a name="BKMK_set_a_data_breakpoint_native_cplusplus"></a>设置数据断点（仅限本机C++）

 当存储在指定内存地址的值发生更改时，数据断点将中断执行。 如果只读取但不更改该值，则执行不会中断。

**要设置数据断点：**

1. 在C++项目中，开始调试，然后等待到达断点。 在 **"调试"** 菜单上，**选择"新建断点** > **数据断点"**

    您还可以在 **"断点"** 窗口中选择 **"新** > **数据断点"，** 或在 **"自动**"、"**监视**"或 **"局部变量"** 窗口中右键单击项目，并在上下文菜单中**的值更改时选择"中断**"。

2. 在“地址”框中，键入内存地址或计算结果为内存地址的表达式****。 例如，键入 `&avar` 以在变量 `avar` 的内容更改时执行中断操作。

3. 在 **“字节计数”** 下拉菜单中，选择你想要调试程序监视的字节数。 例如，如果选择 **4**，则调试程序将监视从 `&avar` 开始的四个字节，并在其中任何字节的值发生更改时执行中断操作。

在以下条件下，数据断点不起作用：
- 将未经调试的进程写入内存位置。
- 在两个或多个进程间共享内存位置。
- 内存位置在内核内更新。 例如，如果内存传递到 32 位 Windows`ReadFile`函数，则内存将从内核模式更新，因此调试器不会在更新时中断。
- 监视表达式在 32 位硬件上大于 4 字节，在 64 位硬件上大于 8 字节。 这是 x86 体系结构的限制。

> [!NOTE]
> - 数据断点取决于特定的内存地址。 变量的地址从一个调试会话更改为下一个调试会话，因此数据断点在每个调试会话结束时会自动禁用。
>
> - 如果在局部变量上设置数据断点，则断点在函数结束时仍处于启用状态，但内存地址不再适用，因此断点的行为不可预测。 如果在局部变量上设置数据断点，则应在函数结束之前删除或禁用断点。

## <a name="manage-breakpoints-in-the-breakpoints-window"></a><a name="BKMK_Specify_advanced_properties_of_a_breakpoint_"></a>在“断点”窗口中管理断点

 您可以使用 **"断点"** 窗口查看和管理解决方案中的所有断点。 此集中式位置在大型解决方案或关键断点的复杂调试方案中特别有用。

在 **"断点"** 窗口中，您可以搜索、排序、筛选、启用/禁用或删除断点。 您还可以设置条件和操作，或添加新函数或数据断点。

要打开**断点**窗口，请选择 **"调试** > **Windows** > **断点**"，或按**Alt**+**F9**或**Ctrl**+**Alt**+**B**。

![断点窗口](../debugger/media/breakpointswindow.png "“断点”窗口")

要选择要在 **"断点"** 窗口中显示的列，请选择"**显示列**"。 选择一个列标题，按该列对断点列表进行排序。

### <a name="breakpoint-labels"></a><a name="BKMK_Set_a_breakpoint_at_a_function_return_in_the_Call_Stack_window"></a> 断点标签
您可以使用标签对**断点**窗口中的断点列表进行排序和筛选。

1. 要向断点添加标签，请右键单击源代码或**断点**窗口中的断点，然后选择 **"编辑标签**"。 添加新标签或选择现有标签，然后选择 **"确定**"。
2. 通过选择 **"标签**、**条件**"或其他列标题，对**断点**窗口中的断点列表进行排序。 您可以通过在工具栏中选择 **"显示列**"来选择要显示的列。

### <a name="export-and-import-breakpoints"></a>导入和导出断点
 要保存或共享断点的状态和位置，可以导出或导入它们。

- 要将单个断点导出到 XML 文件，请右键单击源代码或**断点**窗口中的断点，然后选择"**导出**"或 **"导出所选**"。 选择导出位置，然后选择 **"保存**"。 默认位置是解决方案文件夹。
- 要导出多个断点，请在 **"断点"** 窗口中选择断点旁边的框，或在 **"搜索"** 字段中输入搜索条件。 选择"**导出与当前搜索条件匹配的所有断点**"图标，然后保存该文件。
- 要导出所有断点，请取消选择所有框，并将 **"搜索"** 字段留空。 选择"**导出与当前搜索条件匹配的所有断点**"图标，然后保存该文件。
- 要导入断点，请在 **"断点"** 窗口中，**从文件图标中选择"导入断点**"，导航到 XML 文件位置，然后选择 **"打开**"。

## <a name="set-breakpoints-from-debugger-windows"></a><a name="BKMK_Set_a_breakpoint_from_debugger_windows"></a>从调试器窗口设置断点

您还可以从**调用堆栈**和**拆卸**调试器窗口中设置断点。

### <a name="set-a-breakpoint-in-the-call-stack-window"></a>在呼叫堆栈窗口中设置断点

 要断开调用函数返回的指令或线路，可以在**调用堆栈**窗口中设置断点。

**要在"调用堆栈"窗口中设置断点，**

1. 要打开 **"调用堆栈"** 窗口，必须在调试期间暂停。 选择**调试** > **Windows** > **调用堆栈**，或按**Ctrl**+**Alt**+**C**。

2. 在 **"调用堆栈"** 窗口中，右键单击调用函数并**选择断点** > **插入断点**，或按**F9**。

   在调用堆栈的左边距中，函数调用名称旁边会出现断点符号。

调用堆栈断点在**断点**窗口中显示为地址，内存位置对应于函数中的下一个可执行指令。

调试器在指令处中断。

有关调用堆栈的详细信息，请参阅[：使用调用堆栈窗口](../debugger/how-to-use-the-call-stack-window.md)。

要在代码执行期间直观地跟踪断点，请参阅[调试时调用堆栈上的 Map 方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。

### <a name="set-a-breakpoint-in-the-disassembly-window"></a>在拆解窗口中设置断点

1. 要打开 **"拆解"** 窗口，必须在调试期间暂停。 选择 **"调试** > **Windows** > **拆解**"，或按**Alt**+**8**。

2. 在 **"拆卸"** 窗口中，单击要断开的指令的左边距。 您也可以选择它，然后按**F9**，或右键单击并选择**断点** > **插入断点**。

## <a name="see-also"></a>另请参阅

- [什么是调试？](../debugger/what-is-debugging.md)
- [使用可视化工作室编写更好的 C# 代码](../debugger/write-better-code-with-visual-studio.md)
- [首先查看调试](../debugger/debugger-feature-tour.md)
- [在可视化工作室调试器中排除断点](../debugger/troubleshooting-breakpoints.md)
