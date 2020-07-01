---
title: 调试 Python 代码
description: Visual Studio 为 Python 代码提供丰富的调试，包括设置断点、单步执行、检查值、查看异常以及在交互窗口中进行调试。
ms.date: 05/12/2020
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 2fdbd2e7f47e75b4d80d07f6af3a6f998dfd72d6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541149"
---
# <a name="debug-your-python-code"></a>调试 Python 代码

Visual Studio 提供全面的 Python 调试体验，包括附加到正在运行的进程，在监视窗口和即时窗口中计算表达式，检查局部变量、断点、单步执行/单步跳出/单步跳过语句、设置下一语句等  。

另请参阅以下情景特定的调试文章：

- [Linux 远程调试](debugging-python-code-on-remote-linux-machines.md)
- [Python/C++ 混合模式调试](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)
- [混合模式调试的符号](debugging-symbols-for-mixed-mode-c-cpp-python.md)

<a name="debugging-without-a-project"></a>

> [!Tip]
> Visual Studio 中的 Python 支持不含项目进行调试。 打开独立的 Python 文件后，在编辑器中单击右键，选择“开始调试”，Visual Studio 会使用全局默认环境（请参阅 [Python 环境](managing-python-environments-in-visual-studio.md)）且不使用参数启动脚本。 之后，你就获得完整的调试支持。
>
> 若要控制环境和参数，请为代码创建一个项目，使用[根据现有 Python 代码](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files)项目模板即可轻松完成此操作。

<a name="debugging-with-a-project"></a>

## <a name="basic-debugging"></a>基础调试

基础调试工作流包括如以下各节中所述的设置断点、逐句通过代码、检查值以及处理异常。

使用“Debug” > “Start Debugging”命令、工具栏上的“开始”按钮或 F5 键启动调试会话   。 这些操作使用项目的活动环境和任意命令行参数或“项目属性”中已指定的搜索路径（请参阅[项目调试选项](#project-debugging-options)）来启动项目的启动文件（在解决方案资源管理器中以粗体显示） 。 如未设置启动文件，Visual Studio 2017 版本 15.6 及和更高版本将提醒你。早期版本可能打开一个正在运行 Python 解释器的输出窗口，或输出窗口短暂出现和消失。 在任何情况下，请右键单击相应文件，然后选择“设为启动文件”。

> [!Note]
> 调试器始终通过项目的活动 Python 环境启动。 若要更改环境，请按照[为项目选择一个 Python 环境](selecting-a-python-environment-for-a-project.md)中所述，将其他环境更改为活动状态。

### <a name="breakpoints"></a>断点

断点在标记的点处停止执行代码，便于检查程序状态。 若要设置断点，可单击代码编辑器的左边距或右键单击代码行，然后选择“断点” > “插入断点” 。 包含断点的每行上将出现一个红点。

![Visual Studio 中显示的断点](media/debugging-breakpoints.png)

单击红点或右键单击代码行，选择“断点” > “删除断点”可删除断点 。 若不删除断点，也可以使用“Breakpoint” > “Disable Breakpoint”命令禁用断点 。

> [!Note]
> 一直使用其他编程语言的开发人员可能会对 Python 中的某些断点感到吃惊。 在 Python 中，由于整个文件都是可执行代码，因此在加载该文件来处理任何顶级类或函数定义时，Python 都可以运行该文件。 如果设置了断点，你可能会发现调试器通过一个类声明从中间断开。 虽然有点不可思议，但此行为是正确的。

用户可以自定义触发断点的条件，如仅在变量设置为特定值或值范围时中断。 若要设置条件，请右键单击断点的红点，选择“条件”，然后使用 Python 代码创建表达式。 有关 Visual Studio 中此功能的完整详细信息，请参阅[断点条件](../debugger/using-breakpoints.md#breakpoint-conditions)。

设置条件时，还可以设置“操作”并创建一条消息以记录到输出窗口，从而选择性地继续自动执行。 记录消息这一操作会创建一个所谓的“跟踪点”，而不会将日志记录代码直接添加到应用程序：

![使用断点创建跟踪点](media/debugging-tracepoint.png)

### <a name="step-through-code"></a>逐行执行代码

在断点处停止后，可使用多种方法逐句通过代码或在再次中断之前运行代码块。 多个位置和途径可以提供这些命令，包括顶部调试工具栏、“调试”菜单、通过右键单击代码编辑器中的上下文菜单，以及通过键盘快捷方式（但并非所有命令都可以在这些位置提供）：

| 功能 | 击键 | 描述 |
| --- | --- | --- |
| **Continue** | **F5** | 运行代码，到达下一个断点时停止。 |
| **逐语句** | F11 | 运行下一语句并停止。 如果下一语句是对函数的调用，调试器将在调用函数的第一行处停止。 |
| **逐过程** | **F10** | 运行下一语句，包括对函数进行调用（运行其所有代码）并应用任何返回值。 单步跳过允许轻松跳过不需要调试的函数。 |
| **跳出** | Shift+F11 | 运行代码，到达当前函数的结尾，然后执行调用语句。  不需要调试当前函数的其余部分时，可以使用此命令。 |
| **运行到光标处** | Ctrl+F10 | 运行代码，直到编辑器中的插入符号位置。 使用此命令可以轻松跳过不需要调试的代码段。 |
| **设置下一语句** | Ctrl+Shift+F10 | 将代码中的当前运行点更改为插入符号的位置。 此命令允许忽略运行某个代码段，例如，当已知代码出现故障或产生不良副作用时，可使用此命令。 |
| **显示下一语句** | **Alt**+**Num** **&#42;**| 返回到下一个要运行的语句。 已仔细查看代码但不记得调试器停止的位置时，可以使用此命令。 |

### <a name="inspect-and-modify-values"></a>检查和修改值

在调试器中停止时，可检查和修改变量的值。 还可以使用监视窗口监视单个变量，以及自定义表达式。 （请参阅[检查变量](../debugger/debugger-feature-tour.md#inspect-variables-with-the-autos-and-locals-windows)，了解常规详细信息。）

若要使用数据提示查看值，只需将鼠标悬停在编辑器中的任何变量上即可。 可以单击值进行更改：

![Visual Studio 调试器中显示的 DataTips](media/debugging-quick-tips.png)

自动变量窗口（“调试” > “窗口” > “自动变量”）包含接近当前语句的变量和表达式   。 可以在值列中双击或选择值并按 F2 来编辑值：

![Visual Studio 调试器中的“自动”窗口](media/debugging-autos-window.png)

局部变量窗口（“调试” > “窗口” > “局部变量”）显示当前范围内所有可再次编辑的变量   ：

![Visual Studio 调试器中的“局部变量”窗口](media/debugging-locals-window.png)

有关使用自动变量和局部变量的详细信息，请参阅[在自动变量窗口和局部变量窗口中检查变量](../debugger/autos-and-locals-windows.md) 。

通过监视窗口（“调试” > “窗口” > “监视” > “监视 1-4”）可以输入任意 Python 表达式并查看结果    。 每个步骤都重新计算了表达式：

![Visual Studio 调试器中的“监视”窗口](media/debugging-watch-window.png)

有关使用监视的详细信息，请参阅[使用监视窗口和快速监视窗口对变量设置监视](../debugger/watch-and-quickwatch-windows.md)。

检查字符串值（`str`、`unicode`、`bytes` 和 `bytearray` 均被视为用于此目的字符串）时，该值的右侧将显示一个放大镜图标。 单击该图标将在弹出对话框中显示不带引号的字符串值，对话框具有换行和滚动功能，有助于显示长字符串。 此外，选择图标上的下拉箭头可选择纯文本、HTML、XML 和 JSON 可视化效果：

![Visual Studio 调试器中的字符串可视化工具](media/debugging-string-visualizers.png)

HTML、XML 和 JSON 可视化效果显示在单独的弹出窗口中，其中突出显示了语法并采用树状视图。

### <a name="exceptions"></a>异常

如果调试程序时出错，但没有相应的异常处理程序，调试器将在异常点处中断：

![Visual Studio 调试器中的异常弹出](media/debugging-exception-popup.png)

此时，可以检查程序状态，包括调用堆栈。 但是，如果尝试逐句通过代码，将继续引发该异常，直到异常得以处理或程序退出为止。

“调试” > “窗口” > “异常设置”菜单命令将打开一个窗口，可在其中展开“Python 异常”   ：

![Visual Studio 调试器中的“异常”窗口](media/debugging-exception-settings.png)

每个异常的复选框控制引发该异常时调试器是否*始终*中断。 若要针对特定异常更频繁地进行中断，请选中此框。

默认情况下，在源代码中找不到异常处理程序时，大多数异常将中断。 若要更改此行为，请右键单击任何异常并修改“在用户代码中未经处理时继续”选项。 如果想要针对某异常较少地进行中断，请清除此框。

若要配置此列表中未出现的异常，请单击“添加”按钮进行添加。 名称必须与该异常的完整名称匹配。

## <a name="project-debugging-options"></a>项目调试选项

默认情况下，调试器使用标准 Python 启动器且不使用命令行参数和其他特殊路径或条件启动程序。 可通过右键单击解决方案资源管理器中的项目，选择“属性”，然后选择“调试”选项卡来访问该项目的调试属性，从而更改启动选项  。

![Visual Studio 调试器中的项目调试属性](media/debugging-project-properties.png)

### <a name="launch-mode-options"></a>启动模式选项

| 选项 | 描述 |
| --- | --- |
| **标准 Python 启动器** | 使用以可移植 Python（与 CPython、IronPython 和无堆栈 Python 等变量兼容）编写的调试代码。 它提供调试纯 Python 代码的最佳体验。 附加到正在运行的 python.exe 进程时，将使用此启动器。 此外，此启动器还提供针对 CPython 的[混合模式调试](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)，可以无缝地在 C/C++ 代码和 Python 代码之间进行单步执行。 |
| **Web 启动器** | 在启动时启动默认浏览器并启用模板调试。 请参阅[Web 模板调试](python-web-application-project-templates.md#debugging)部分，了解详细信息。 |
| **Django Web 启动器** | 相当于 Web 启动器，仅为了向后兼容性而显示。 |
| **IronPython (.NET) 启动器** | 使用 .NET 调试器，它只适用于 IronPython，但允许在任何 .NET 语言项目（包括 C# 和 VB）之间进行单步执行。 如果附加到托管 IronPython 的正在运行的 .NET 进程，将使用此启动器。 |

### <a name="run-options-search-paths-startup-arguments-and-environment-variables"></a>运行选项（搜索路径、启动参数和环境变量）

| 选项 | 描述 |
| --- | --- |
| **搜索路径** | 这些值与解决方案资源管理器中项目的搜索路径节点中显示的值匹配 。 可以在此处修改该值，但使用解决方案资源管理器更简单，因为可以浏览文件夹和自动将路径转换为相对形式。 |
| **脚本参数** | 这些参数添加到用于启动脚本的命令中，并且显示在脚本的文件名后。 此处可供脚本使用的第一项为 `sys.argv[1]`，第二项为 `sys.argv[2]`，以此类推。 |
| **解释器参数** | 这些参数添加到启动程序命令行中的脚本名称之前。 此处常见的参数有：用于控制警告的 `-W ...`、用于略微优化程序的 `-O` 和用于使用未缓冲 IO的 `-u`。 IronPython 用户可能会使用此字段来传递 `-X` 选项，例如 `-X:Frames` 或 `-X:MTA`。 |
| **解释器路径** | 替代与当前环境相关联的路径。 值可能可用于通过非标准解释器启动脚本。 |
| **环境变量** | 在此多行文本框中，添加 \<NAME>=\<VALUE> 形式的条目。 由于除任何现有全局环境变量外，此设置是最后应用，因此在根据搜索路径设置设定 `PYTHONPATH` 之后，可以将该设置用于手动替代任何其他变量。 |

## <a name="immediate-and-interactive-windows"></a>即时窗口和交互窗口

调试会话期间可使用两个交互窗口：标准 Visual Studio 即时窗口和 Python 调试交互窗口 。

即时窗口（“调试” > “窗口” > “即时”）用于快速计算 Python 表达式以及检查或分配正在运行的程序中的变量   。 请参见常规[即时窗口](../ide/reference/immediate-window.md)一文，了解详细信息。

Python 调试交互窗口（“调试” > “窗口” > “Python 调试交互”）更丰富，因为它可以在调试（包括编写和运行代码）时提供完整的[交互式 REPL](python-interactive-repl-in-visual-studio.md) 体验   。 它会自动连接到使用标准 Python 启动器在调试器中启动的任何进程（包括通过连接“调试” > “附加到进程”附加的进程） 。 但使用 C/C++ 混合模式调试时，它不可用。

![Python 调试交互窗口](media/debugging-interactive.png)

除[标准 REPL 命令](python-interactive-repl-in-visual-studio.md#meta-commands)外，调试交互窗口还支持特殊元命令：

| 命令 | 自变量 | 描述 |
| --- | --- | --- |
| `$continue`, `$cont`, `$c` | 从当前语句开始运行程序。 |
| `$down`，`$d` | 在堆栈跟踪中将当前帧下移一级。 |
| `$frame` | | 显示当前的帧 ID。
| `$frame` | 帧 ID | 将当前帧切换为指定帧 ID。
| `$load` | 从文件加载命令并执行，直到完成 |
| `$proc` |  | 显示当前的进程 ID。 |
| `$proc` | 进程 ID | 将当前进程切换为指定进程 ID。 |
| `$procs` | | 列出当前正在调试的进程。 |
| `$stepin`, `$step`, `$s` | 如果可能，单步执行下一个函数调用。 |
| `$stepout`, `$return`, `$r` | 跳出当前函数。 |
| `$stepover`, `$until`, `$unt` | 转到下一个函数调用。 |
| `$thread` | | 显示当前的线程 ID。 |
| `$thread` | 线程 ID | 将当前线程切换为指定线程 ID。 |
| `$threads` | | 列出当前正在调试的线程。 |
| `$up`，`$u` | | 在堆栈跟踪中将当前帧上移一级。 |
| `$where`, `$w`, `$bt` | 列出当前线程的帧。 |

请注意，标准调试器窗口（如进程、线程和调用堆栈）不与调试交互窗口同步   。 更改调试交互窗口中的活动进程、线程或帧不会影响其他调试器窗口。 同样，更改其他调试器窗口中的活动进程、线程或帧也不会影响调试交互窗口。

<a name="use-the-experimental-debugger"></a>

## <a name="use-the-legacy-debugger"></a>使用旧版调试程序

Visual Studio 2017 版本 15.8 及更高版本使用基于 ptvsd 版本 4.1+ 的调试程序。 Visual Studio 2019 版本 16.5 及更高版本使用基于 debugpy 的调试程序。 这些版本的调试程序与 Python 2.7 和 Python 3.5+ 兼容。 如果使用 Python 2.6、3.1 到 3.4 或 IronPython，Visual Studio 会显示“调试程序不支持此 Python 环境”错误：

![使用调试程序时，出现“调试程序不支持此 Python 环境”错误](media/debugging-experimental-incompatible-error.png)

在这些情况下，必须使用较早的调试程序（Visual Studio 2017 版本 15.7 及更早版本中的默认调试程序）。 选择“工具” > “选项”菜单命令，导航到“Python” > “调试”，然后选择“使用旧版调试程序”选项    。

如果已在当前环境中安装了旧版本的 ptvsd（例如早期的 4.0.x 版本或远程调试所需的 3.x 版本），则 Visual Studio 会显示错误或警告。

安装 ptvsd 3.x 时，出现“无法加载调试程序包”错误：

![使用调试程序时，出现“无法加载调试程序包”错误](media/debugging-experimental-version-error.png)

在这种情况下，请选择“使用旧版调试程序”来设置“使用旧版调试程序”选项，然后重启调试程序 。

安装早期 4.x 版本的 ptvsd 时，出现“调试程序包已过时”警告：

![使用调试程序时，出现“调试程序包已过时”警告](media/debugging-experimental-version-warning.png)

> [!Important]
> 虽然可以选择忽略某些 ptvsd 版本的警告，但 Visual Studio 可能无法正常运行。

管理 ptvsd 安装：

1. 导航到“Python 环境”窗口中的“包”选项卡 。

1. 在搜索框中输入“ptvsd”并检查已安装的 ptvsd 版本：

    ![在“Python 环境”窗口中检查 ptvsd 版本](media/debugging-experimental-check-ptvsd.png)

1. 如果版本低于 4.1.1a9（与 Visual Studio 捆绑的版本），请选择包右侧的“X”以卸载旧版本。 随后，Visual Studio 使用其捆绑版本。 （也可使用 `pip uninstall ptvsd` 从 PowerShell 卸载。）

1. 也可以按照[疑难解答](#troubleshooting)部分中的说明操作，将 ptvsd 包更新为最新版本。

## <a name="troubleshooting"></a>疑难解答

### <a name="for-visual-studio-2019-version-164-and-earlier-upgrade-ptvsd"></a>对于 Visual Studio 2019（版本 16.4 及更早版本）升级 ptvsd
如果无法使用调试器，请先升级调试器版本，步骤如下：

1. 导航到“Python 环境”窗口中的“包”选项卡 。

1. 在搜索框中输入“`ptvsd --upgrade`”，再选择“运行命令: pip install ptvsd --upgrade”。 （也可使用 PowerShell 中的相同命令。）

    ![在 Python 环境窗口中提供 ptvsd 升级命令](media/debugging-experimental-upgrade-ptvsd.png)

   如果此问题一再出现，请在 [PTVS GitHub 存储库](https://github.com/Microsoft/ptvs/issues)中提交问题。

   > [!NOTE]
   > 对于 Visual Studio 2019 版本 16.5 及更高版本，debugpy 是 Visual Studio Python 工作负载的一部分，与 Visual Studio 一起更新。

### <a name="enable-debugger-logging"></a>启用调试器日志记录

在调查调试器问题的过程中，Microsoft 可能会要求你启用并收集有助于诊断的调试器日志。

若要在当前 Visual Studio 会话中启用调试，请按照以下步骤操作：

1. 依次使用“视图” > “其他 Windows” > “命令窗口”菜单命令，在 Visual Studio 中打开命令窗口。

1. 输入以下命令：

    ```ps
    DebugAdapterHost.Logging /On /OutputWindow
    ```

1. 开始调试并完成重现问题所需的任何步骤。 在此期间，调试日志显示在“调试适配器主机日志”下的“输出”窗口中。 然后，可以将日志从此窗口中复制并粘贴到 GitHub 问题、电子邮件等中。

    ![“输出”窗口中的调试器日志记录输出](media/debugger-logging-output.png)

1. 如果 Visual Studio 挂起或你无法以其他方式访问“输出”窗口，请重启 Visual Studio，打开命令窗口，并输入以下命令：

    ```ps
    DebugAdapterHost.Logging /On
    ```

1. 开始调试并再次重现问题。 然后，可以在 `%temp%\DebugAdapterHostLog.txt` 中找到调试器日志。

## <a name="see-also"></a>请参阅

有关 Visual Studio 调试器的完整详细信息，请参阅 [Visual Studio 中的调试](../debugger/debugger-feature-tour.md)。
