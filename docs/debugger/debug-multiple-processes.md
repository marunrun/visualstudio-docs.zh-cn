---
title: 调试多个进程 | Microsoft Docs
ms.date: 11/20/2018
ms.topic: how-to
f1_keywords:
- vs.debug.programs
- vs.debug.processes.attaching
- vs.debug.activeprogram
- vs.debug.attaching
- vs.debug.attachedprocesses
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: bde37134-66af-4273-b02e-05b3370c31ab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94a61e0083b17fa095b419a2066a4f8b9c39dfb7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350597"
---
# <a name="debug-multiple-processes-c-visual-basic-c"></a>调试多个进程（C#、Visual Basic、C++）

Visual Studio 可以调试具有多个进程的解决方案。 可以启动和切换进程、中断、继续和逐步执行源代码、停止调试以及结束单个进程或与进程分离。

## <a name="start-debugging-with-multiple-processes"></a>开始调试多个进程

当 Visual Studio 解决方案中有多个项目可以独立运行时，可以选择调试器启动的项目。 当前启动项目以粗体显示在“解决方案资源管理器”中。

若要更改启动项目，请在“解决方案资源管理器”中，右键单击其他项目并选择“设为启动项目” 。

若要从“解决方案资源管理器”中开始调试项目，而不将它设为启动项目，请右键单击该项目并选择“调试” > “启动新实例”或“进入并单步执行新实例”。

若要通过解决方案属性设置启动项目或多个项目：

1. 在“解决方案资源管理器”中选择解决方案，然后选择工具栏中的“属性”图标，或右键单击解决方案并选择“属性”  。

1. 在“属性”页中，选择“公共属性” > “启动项目”。

   ![为项目更改启动类型](../debugger/media/dbg_execution_startmultipleprojects.png "DBG_Execution_StartMultipleProjects")

1. 选择“当前选择”、“单启动项目”和项目文件，或“多启动项目”。

   如果选择“多启动项目”，则可以为每个项目更改启动顺序和要执行的操作：“启动”、“在不调试的情况下启动”或“无”。

1. 选择“应用”或“确定”以应用并关闭对话框。

### <a name="attach-to-a-process"></a><a name="BKMK_Attach_to_a_process"></a>附加到进程

调试器还可以附加到在 Studio 外部运行（包括在远程设备上）的应用。 附加到应用之后，可以使用 Visual Studio 调试器。 调试功能可能会受到限制。 这取决于应用是否是使用调试信息生成、你是否有权访问应用的源代码以及 JIT 编译器是否跟踪调试信息。

有关详细信息，请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

**附加到正在运行的进程：**

1. 在应用正在运行的情况下，选择“调试” > “附加到进程” 。

   ![“附加到进程”对话框](../debugger/media/dbg_attachtoprocessdlg.png "“附加到进程”对话框")

1. 在“附加到进程”对话框中，从“可用进程”列表中选择进程，然后选择“附加”。

>[!NOTE]
>调试器不会自动附加到调试进程所启动的子进程中，即使子项目位于同一个解决方案中。 若要调试子进程，请在启动子进程之后附加到它，或配置 Windows 注册表编辑器以在新调试器实例中启动子进程。

### <a name="use-the-registry-editor-to-automatically-start-a-process-in-the-debugger"></a><a name="BKMK_Automatically_start_an_process_in_the_debugger"></a> 使用注册表编辑器在调试器中自动启动进程

有时，你可能需要调试由另一个进程启动的应用的启动代码。 这样的示例包括服务和自定义设置操作。 可以让调试器启动并自动附加到应用。

1. 通过运行 regedit.exe 来启动 Windows 注册表编辑器。

1. 在注册表编辑器中，导航到 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options。

1. 选择要在调试器中启动的应用程序的文件夹。

   如果应用未列出为子文件夹，请右键单击“Image File Execution Options”，选择“新建” > “项”，然后键入应用名称。 或者，在树中右键单击新项，选择“重命名”，然后输入应用名称。

1. 在树中右键单击新项，然后选择“新建” > “字符串值”。

1. 将新值的名称从“新值 #1”更改为 `debugger`。

1. 右键单击 debugger 并选择“修改”。

   ![“编辑字符串”对话框](../debugger/media/dbg_execution_automaticstart_editstringdlg.png "“编辑字符串”对话框")

1. 在“编辑字符串”对话框的“数值数据”框中，键入 `vsjitdebugger.exe`，然后选择“确定”。

   ![regedit.exe 中的自动调试器启动条目](../debugger/media/dbg_execution_automaticstart_result.png "regedit.exe 中的自动调试器启动条目")

## <a name="debug-with-multiple-processes"></a><a name="BKMK_Switch_processes__break_and_continue_execution__step_through_source"></a> 使用多个进程调试
<a name="BKMK_Configure_the_execution_behavior_of_multiple_processes"></a>

当调试具有多个进程的应用时，默认情况下，中断、单步执行和继续调试器命令会影响所有进程。 例如，当某个进程在断点处暂停时，所有其他进程的执行也会暂停。 可更改此默认行为以获取对执行命令的目标的更多控制。

若要更改在一个进程中断时是否暂停所有进程，请执行以下操作：

- 在“工具”（或“调试”）>“选项” > “调试” > “常规”下，选中或清除“一个进程中断时则中断所有进程”复选框。

### <a name="break-step-and-continue-commands"></a><a name="BKMK_Break__step__and_continue_commands"></a>中断、单步执行和继续命令

下表介绍在选中或取消选中“一个进程中断时则中断所有进程”复选框时调试命令的行为：

|**命令**|已选定|取消选择|
|-|-|-|
|“调试”  > “全部中断”|所有进程中断。|所有进程中断。|
|“调试” > “继续”|所有进程继续。|所有挂起的进程继续。|
|“调试” > “单步执行”、“逐过程”或“跳出”|在当前进程单步执行时，所有进程将运行。 <br />然后，所有进程中断。|当前进程单步执行。 <br />已挂起的进程继续。 <br />正在运行的进程继续。|
|“调试” > “进入并单步执行当前进程”、“逐过程执行当前进程”或“跳出当前进程”|不可用|当前进程单步执行。<br />其他进程保持其现有状态（挂起或运行）。|
|源窗口“断点”|所有进程中断。|仅源窗口进程中断。|
|源窗口“运行到光标处”<br />源窗口必须在当前进程中。|当源窗口进程运行到光标处所有进程运行，然后中断。<br />然后，所有其他进程中断。|源窗口进程运行到光标处。<br />其他进程保持其现有状态（挂起或运行）。|
|“进程”窗口 >“中断进程”|不可用|已选进程中断。<br />其他进程保持其现有状态（挂起或运行）。|
|“进程”窗口 >“继续进程”|不可用|已选进程继续。<br />其他进程保持其现有状态（挂起或运行）。|

### <a name="find-the-source-and-symbol-pdb-files"></a><a name="BKMK_Find_the_source_and_symbol___pdb__files"></a>查找源文件和符号 (.pdb) 文件
若要浏览进程的源代码，调试器需要访问其源文件和符号文件。 有关详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

如果无法访问进程的文件，则可使用“反汇编”窗口进行导航。 有关详细信息，请参阅[如何：使用“反汇编”窗口](../debugger/how-to-use-the-disassembly-window.md)。

### <a name="switch-between-processes"></a><a name="BKMK_Switch_between_processes"></a>在进程之间切换

调试时可以附加到多个进程，但在任何给定时间，调试器中只有一个进程处于活动状态。 可以在“调试位置”工具栏或“进程”窗口中设置活动的或当前的进程 。 若要在两个进程间切换，这两个进程必须处于中断模式。

若要从“调试位置”工具栏设置当前进程，请执行以下操作：

1. 若要打开“调试位置”工具栏，请选择“查看” > “工具栏” > “调试位置”。

1. 调试过程中，在“调试位置”工具栏上，从“进程”下拉菜单中选择要设置为当前进程的进程。

   ![在进程之间切换](../debugger/media/dbg_execution_switchbetweenmodules.png "DBG_Execution_SwitchBetweenModules")

若要从“进程”窗口设置当前进程，请执行以下操作：

1. 若要在调试期间打开“进程”窗口，请选择“调试” > “窗口” > “进程”。

1. 在“进程”窗口中，当前进程由黄色箭头标记。 双击要设置为当前进程的进程。

   ![“进程”窗口](../debugger/media/dbg_processeswindow.png "DBG_ProcessesWindow")

切换到一个进程将它设置为用于调试目的的当前进程。 调试器窗口会显示当前进程的状态，并且单步执行命令将仅影响当前进程。

## <a name="stop-debugging-with-multiple-processes"></a>停止调试多个进程

默认情况下，当选择“调试” > “停止调试”时，调试器会结束所有进程或从它们分离。

- 如果在调试器中启动了当前进程，则该进程会结束。

- 如果您已将调试器附加到当前进程，则调试器会与进程分离并使进程保持运行。

如果从 Visual Studio 解决方案中开始调试进程，然后将其附加到另一个已运行的进程，然后选择“停止调试”，则调试会话将结束。 在 Visual Studio 中启动的进程会结束，而附加的进程会保持运行。

若要控制“停止调试”影响单个进程的方式，请在“进程”窗口中，右键单击某个进程，然后选中或清除“调试停止时分离”复选框。

>[!NOTE]
>“一个进程中断时则中断所有进程”调试器选项不影响停止、终止或从进程分离。

### <a name="stop-terminate-and-detach-commands"></a>停止、终止和分离命令

下表介绍调试器停止、终止和分离命令对多个进程的行为：

|**命令**|**说明**|
|-|-|
|“调试” > “停止调试”|除非在“进程”窗口中更改了行为，否则调试器启动的进程会结束，附加的进程会分离。|
|“调试” > “全部终止”|所有进程都会结束。|
|“调试” > “全部分离”|调试器与所有进程分离。|
|“进程”窗口 >“分离进程”|调试器与选定进程分离。<br />其他进程保持其现有状态（挂起或运行）。|
|“进程”窗口 >“终止进程”|所选进程会结束。<br />其他进程保持其现有状态（挂起或运行）。|
|“进程”窗口 >“调试停止时分离”|如果选择，则“调试” > “停止调试”会从所选进程分离。 <br />如果未选择，则“调试” > “停止调试”会结束所选进程。 |

## <a name="see-also"></a>请参阅

- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)
- [实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)
- [调试多线程应用](../debugger/debug-multithreaded-applications-in-visual-studio.md)