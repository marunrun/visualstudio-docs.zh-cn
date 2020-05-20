---
title: 适用于 R 的交互式 REPL
description: 如何为 Visual Studio 中的 R 使用交互 REPL 环境（已与编辑器窗口集成）。
ms.date: 06/28/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 7109e74e858aa308b8f49e6e1e335478f801070b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62814852"
---
# <a name="work-with-the-r-interactive-window"></a>使用 R 交互窗口

针对 Visual Studio 的 R 工具 (RTVS) 提供了一个 R 交互窗口，也称为 REPL  （读取-求值-打印-循环）窗口，可在其中输入 R 代码并立即查看结果。 所有模块、语法、变量以及 IntelliSense 都可在该交互窗口中使用。

交互窗口还与常规 R 编辑器窗口集成。 可选择代码并按 Ctrl+Enter，也可右键单击并选择“交互执行”，代码将在交互窗口中逐行运行，就像直接键入一样。 如果光标位于编辑器窗口中的某一行上，则按 Ctrl+Enter 将该行发送至交互窗口，然后将光标移到下一行。 这样，只需重复按 Ctrl+Enter 即可逐行执行代码。

要体验这些功能，可按照 [R 入门](getting-started-with-r.md)演练及本文中的相关部分进行操作。 [代码片段](code-snippets-for-r.md)在交互窗口中的运行方式与在 R 编辑器窗口中的运行方式一样。

## <a name="overview-of-the-interactive-window"></a>交互窗口概述

在代码行末尾键入有效的 R 代码，按 Enter 可以运行该行代码  ：

```repl
> 3 + 3
[1] 6
```

在单行输入中的任意位置按 Enter，也会运行该代码行  。

REPL 中以前的所有输入和输出都是只读的，不能更改。 但是，随时都可从窗口中复制并粘贴文本。 粘贴的代码会像逐行输入的代码一样运行。

也就是说，如果开始键入语句并按 Enter，RTVS 将知道语句何时需要继续，并通过左侧的 + 提示和适当的缩进进入多行模式  。 RTVS 还会使用成对的圆括号、方括号和大括号：

![交互窗口中的多行语句条目](media/repl-multiline-entry.png)

在这个多行模式下，仅当位于代码块末尾时，按 Enter 才会运行该代码块，否则将插入新行  。 但是，可在任意位置按 Ctrl+Enter 来立即运行代码块。

### <a name="toolbar-commands"></a>工具栏命令

以下是交互窗口及其工具栏：

![交互窗口与工具栏](media/repl-window.png)

工具栏命令如下所示，其中多数命令具有键盘等效项，并且可在“R 工具” > “会话”和“R 工具” > “工作目录”菜单中获取（或如上所述）：

| Button | 命令 | 组合键 | 说明 |
| --- | --- | --- | --- |
| ![“重置”按钮](media/repl-toolbar-01-reset.png) | 重置 |  Ctrl+  Shift+  F10 | 重置交互窗口会话，清除所有变量和历史记录。 |
| ![“清除”按钮](media/repl-toolbar-02-clear.png) | 清除 |  Ctrl + L  | 清除交互窗口中显示的输出，不影响会话变量或历史记录。 |
| ![“历史记录”按钮](media/repl-toolbar-03-history.png) | “上一条历史记录”命令<br/>“下一条历史记录”命令 | 向上，向下  <br/>Alt+向上键，Alt+向下键 | 滚动浏览历史记录，以及多行代码块的某些行为。 请参阅[历史记录](#history)。 |
| ![“加载工作区”按钮](media/repl-toolbar-04-load-workspace.png) | 加载工作区 | n/a | 加载以前保存的工作区（请参阅[工作区和会话](#workspaces-and-sessions)。 |
| ![“工作区另存为”按钮](media/repl-toolbar-05-save-workspace-as.png)| 工作区另存为 | n/a | 将当前状态的会话另存为工作区（请参阅[工作区和会话](#workspaces-and-sessions)。 |
| ![“源化 R 脚本”按钮](media/repl-toolbar-06-source-r-script.png) | 源化 R 脚本 |  Ctrl + Shift  **S**+  | 在 Visual Studio 编辑器中使用当前活动的 R 脚本调用 `source`，它将运行代码。  仅当在 Visual Studio 编辑器中打开 R 文件时，才会显示此按钮。 |
| ![“源化带有回响的 R 脚本”按钮](media/repl-toolbar-07-source-r-script-with-echo.png) | 源化带有回响的 R 脚本 | Ctrl+Shift+Enter | 与源化 R 脚本相同，但在交互窗口中显示脚本内容。 |
| ![“中断 R”按钮](media/repl-toolbar-08-interrupt-r.png)| 中断 R | Esc  | 停止交互窗口中任何正在运行的代码，如该部分开头的屏幕截图中的 `while` 循环。 |
| ![“附加调试器”按钮](media/repl-toolbar-09b-attach-debugger.png)| 附加调试器 | n/a | 也可使用“调试” > “附加到 R 交互”命令。 |
| ![“将工作目录设置为源文件位置”按钮](media/repl-toolbar-10-set-working-directory-source.png)| 将工作目录设置为源文件位置 | Ctrl+Shift+E | （使用 `source`）将工作目录设置为加载到交互窗口的最新源文件。 请参阅[工作目录](#working-directory)。 |
| ![“将工作目录设置为项目位置”按钮](media/repl-toolbar-11-set-working-directory-to-project.png) | 将工作目录设置为项目位置 | Ctrl+Shift+P | 将工作目录设置为 Visual Studio 中当前加载项目的根目录。 请参阅[工作目录](#working-directory)。 |
| (文本字段) | 选择工作目录 | n/a | 工作目录的直接输入字段。 请参阅[工作目录](#working-directory)。 |

## <a name="workspaces-and-sessions"></a>工作区和会话

在交互窗口中运行代码会在当前会话中生成上下文。 上下文由全局变量、函数定义、库加载等组成。 这个上下文统称为“工作区”  ，可随时保存和加载工作区。

如果选择“工作区另存为”按钮或使用“R 工具” > “会话” > “工作区另存为”命令，系统会提示你输入位置和文件名（默认扩展名为 .RData）。

要使用特定文件名（默认为 .RData）保存工作区，请单击 REPL 中的“保存工作区”按钮   ：

要重新加载之前保存的工作区，请选择“加载工作区”按钮，或使用“R 工具” > “会话” > “加载工作区”并导航到工作区文件。

使用“重置”按钮或“R 工具” > “会话” > “重置”，可清除会话上下文。 如果使用远程会话，重置操作还会删除远程计算机上的用户配置文件，清除其中存储的所有文件。 （请参阅[工作区](r-workspaces-in-visual-studio.md#directories-on-local-and-remote-computers)。）

## <a name="working-directory"></a>工作目录

开发人员通常想要在进行交互会话时更改其工作目录。 工具栏、“R 工具” > “工作目录”菜单和项目上下文菜单中提供了许多命令，它们可用于轻松地将工作目录设置为源文件位置、项目位置或其他任意位置。 这样做有助于避免在引用文件时键入完整路径或冗长的相对路径。

## <a name="history"></a>历史记录

在交互窗口中输入的每行代码（包括从编辑器发送的代码行）都将保留在 REPL 的历史记录中。 然后，可以使用向上键和向下键浏览历史记录，就像使用命令行时可能习惯进行的操作一样。

区别在于，如果在当前行上开始键入，并按向上键，即使尚未运行该行，它也将保留在历史记录中。

交互窗口中的历史记录还会智能地与其他跨行代码块的语句进行协作。 如果使用向上键和向下键循环浏览历史记录，将以整体单位的形式检索多行代码块，并且这些代码块将显示为当前项。 此时，使用箭头键可逐行浏览代码块，直到到达顶部或底部。 在代码块顶部，使用向上键将检索上一条历史记录项，而在底部，使用向下键将检索下一条历史记录。

此行为的一个典型用例是：使用向上键和 Enter 键击组合重新运行上一条历史记录，同时通过按向上键导航到多行代码块中，自然允许对该代码块进行编辑  。

要避免导航到多行代码块中，可使用工具栏按钮或 Alt+向上键和 Alt-向下键，这样所有此类代码块均将被视为单行。

体验历史记录功能的最简单方式是亲自在交互窗口中尝试。 以下代码可提供多个适合的单行语句和多行语句。 但是，请单独复制粘贴每个语句，创建相应的历史记录。 （还可将代码粘贴到单独的代码文件中，然后使用 Ctrl+Enter 将其发送到交互窗口。）

```R
3 + 3

4 + 4

5 + 5

add <- function (x, y) {
  return (x + y)
}

sub <- function (x, y) {
  return (x - y)
}
```