---
title: 命令别名
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- aliases, Visual Studio commands
- Visual Studio, commands
- predefined command aliases
- commands, aliases
- Visual Studio commands
- pre-defined command aliases
- command aliases
ms.assetid: de8bb378-8c1c-4087-a9a5-537fa8314c19
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b420644672309371ab61f1499e22d4745c69c569
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596406"
---
# <a name="visual-studio-command-aliases"></a>Visual Studio Command Aliases

通过命令别名，可在希望执行命令时键入较少的字符。 可将别名输入“查找/命令”  框或“命令”  窗口。 例如，可以使用预定义别名 `>File.OpenFile`，而不是输入  **来显示“打开文件”** `>of`对话框。

在“命令”`alias`**窗口中键入**  可显示当前别名及其定义的列表。 键入 `>cls` 可清除“命令”  窗口中的内容。 若要查看特定命令的别名，请键入 `alias <command name>`。

您可以轻松地为某个 Visual Studio 命令创建您自己的别名（带有或不带参数）。 例如，用于为 `File.NewFile MyFile.txt` 创建别名的语法是 `alias MyAlias File.NewFile MyFile.txt`。 您可以使用 `alias <alias name> /delete` 删除某个别名。

下表包含预定义的 Visual Studio 命令别名的列表。 某些命令名称具有多个预定义的别名。 单击下面的命令名称链接可显示详细的主题信息，其中介绍了这些命令的正确语法、参数和开关。

|命令名：|Alias|完整名称|
|------------------|-----------|-------------------|
|[“打印”命令](../../ide/reference/print-command.md)|?|Debug.Print|
|[“快速监视”命令](../../ide/reference/quick-watch-command.md)|??|Debug.Quickwatch|
|添加新项目|AddProj|File.AddNewProject|
|[“别名”命令](../../ide/reference/alias-command.md)|Alias|Tools.Alias|
|“自动”窗口|自动|调试.自动窗口|
|“断点”窗口|bl|调试.断点|
|切换断点|bp|Debug.ToggleBreakPoint|
|“调用堆栈”窗口|CallStack|调试.调用堆栈|
|清除书签|ClearBook|编辑.清除书签|
|关闭|关闭|File.Close|
|关闭所有文档|CloseAll|Window.CloseAllDocuments|
|全部清除|cls|Edit.ClearAll|
|命令模式|cmd|视图.命令窗口|
|查看代码|代码|视图.查看代码|
|[“列出内存”命令](../../ide/reference/list-memory-command.md)|d|Debug.ListMemory|
|[“列出内存”命令](../../ide/reference/list-memory-command.md)（按 ANSI）|da|Debug.ListMemory /Ansi|
|[“列表内存”命令](../../ide/reference/list-memory-command.md)（1 字节格式）|db|Debug.ListMemory /Format:OneByte|
|[“列出内存”命令](../../ide/reference/list-memory-command.md)（按照 ANSI 4 字节格式）|dc|Debug.ListMemory /Format:FourBytes /Ansi|
|[“列表内存”命令](../../ide/reference/list-memory-command.md)（4 字节格式）|dd|Debug.ListMemory /Format:FourBytes|
|删除到行首|DelBOL|Edit.DeleteToBOL|
|删除到行尾|DelEOL|Edit.DeleteToEOL|
|删除水平空白|DelHSp|Edit.DeleteHorizontalWhitespace|
|视图设计器|设计器|视图.视图设计器|
|[“列表内存”命令](../../ide/reference/list-memory-command.md)浮动格式|df|Debug.ListMemory/Format:Float|
|“反汇编”窗口|disasm|调试.反汇编|
|[“列表内存”命令](../../ide/reference/list-memory-command.md)（8 字节格式）|dq|Debug.ListMemory /Format:EightBytes|
|[“列出内存”命令](../../ide/reference/list-memory-command.md)（按 Unicode）|du|Debug.ListMemory /Unicode|
|[“计算语句”命令](../../ide/reference/evaluate-statement-command.md)|eval|Debug.EvaluateStatement|
|Exit|Exit|文件.退出|
|设置选定内容的格式|format|编辑.格式化选定内容|
|全屏显示|全屏|视图.全屏|
|[“启动”命令](../../ide/reference/start-command.md)|g|调试.启动|
|[“转到”命令](../../ide/reference/go-to-command.md)|GotoLn|编辑.转到|
|转到大括号|GotoBrace|编辑.转到大括号|
|F1Help|帮助|帮助.F1 帮助|
|即时模式|immed|Tools.ImmediateMode|
|将文件作为文本插入|InsertFile|Edit.InsertFileAsText|
|[“列出调用堆栈”命令](../../ide/reference/list-call-stack-command.md)|kb|Debug.ListCallStack|
|转换为小写|Lcase|编辑.转换为小写|
|剪切行|LineCut|编辑.剪切行|
|删除行|LineDel|编辑.删除行|
|列表成员|ListMembers|编辑.列出成员|
|局部变量窗口|局部变量|调试.局部变量|
|[“日志命令窗口输出”命令](../../ide/reference/log-command-window-output-command.md)|日志|Tools.LogCommandWindowOutput|
|“命令”窗口“标记”模式|mark|Tools.CommandWindowMarkMode|
|“内存”窗口|Memory Memory1|调试.内存1|
|“内存”窗口 2|Memory2|调试.内存2|
|“内存”窗口 3|Memory3|调试.内存3|
|“内存”窗口 4|Memory4|调试.内存4|
|[“设置基数”命令](../../ide/reference/set-radix-command.md)|n|Debug.SetRadix|
|[ShowWebBrowser 命令](../../ide/reference/showwebbrowser-command.md)|nav navigate|View.ShowWebBrowser|
|下一书签|NextBook|编辑.下一书签|
|[“新建文件”命令](../../ide/reference/new-file-command.md)|nf|文件.新建文件|
|新建项目|np NewProj|文件.新建项目|
|[“打开文件”命令](../../ide/reference/open-file-command.md)|of Open|文件.打开文件|
|[“打开项目”命令](../../ide/reference/open-project-command.md)|op|文件.打开项目|
|折叠到定义/停止大纲显示|OutlineDefs StopOutlining|Edit.CollapseToDefinitions|
|逐过程|p|调试.逐过程|
|参数信息|ParamInfo|编辑.参数信息|
|跳出|pr|调试.跳出|
|上一书签|PrevBook|编辑.上一书签|
|打印文件|print|文件.打印|
|“属性”窗口|props|视图.属性窗口|
|停止|q|调试.停止调试|
|重做|重做 (redo)|编辑.重做|
|“寄存器”窗口|寄存器|调试.寄存器|
|运行到光标处|rtc|调试.运行到光标处|
|保存选定项|保存|文件.保存选定项|
|全部保存|SaveAll|文件.全部保存|
|另存为|SaveAs|File.SaveSelectedItemsAs|
|[Shell 命令](../../ide/reference/shell-command.md)|shell|Tools.Shell|
|停止“在文件中查找”|StopFind|Edit.FindInFiles /stop|
|交换定位点|SwapAnchor|编辑.交换定位点|
|逐语句|t|调试.逐语句|
|将选定内容替换为制表符|替换为制表符|Edit.TabifySelection|
|“任务列表”窗口|TaskList|视图.任务列表|
|“线程”窗口|线程|调试.线程|
|水平平铺|TileH|Window.TileHorizontally|
|垂直平铺|TileV|Window.TileVertically|
|切换书签|ToggleBook|编辑.切换书签|
|工具箱窗口|工具箱|视图.工具箱|
|[“列出反汇编”命令](../../ide/reference/list-disassembly-command.md)|u|Debug.ListDisassembly|
|转换为大写|Ucase|编辑.转换为大写|
|撤消|撤消|编辑.取消|
|将所选内容中的制表符替换为空格|Untabify|Edit.UntabifySelection|
|监视窗口|监视|Debug.WatchN|
|切换自动换行|WordWrap|编辑.切换自动换行|
|列出进程|&#124;|Debug.ListProcesses|
|[“列出线程”命令](../../ide/reference/list-threads-command.md)|~ ~*k ~\*kb|Debug.ListThreads Debug.ListTheads /AllThreads|

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
