---
title: Python 交互式窗口 (REPL)
description: 使用交互式窗口 (REPL) 在 Visual Studio 中进行快速 Python 代码开发。
ms.date: 02/11/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 7ceecffec577528484cd67fd13d3e04f368fb916
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307111"
---
# <a name="work-with-the-python-interactive-window"></a>使用 Python 交互窗口

Visual Studio 为每个 Python 环境提供交互读取-评估-打印-循环 (REPL) 窗口，改进了在命令行中运行 python.exe  获得的 REPL。 借助交互  窗口（通过“视图”   > “其他窗口”   > “&lt;环境&gt;交互”  菜单命令打开），可以输入任意 Python 代码，并查看即时结果。 这种编码方式有助于了解与实验 API 和库，并以交互方式开发要包含在项目中的工作代码。

![Python 交互窗口](media/interactive-window.png)

Visual Studio 有大量 Python REPL 模式可供选择：

| REPL | 描述 | 编辑 | 调试 | 映像 |
| --- | --- | --- | --- | --- |
| 标准 | 默认 REPL，直接与 Python 通信 | 标准编辑（多行等）。 | 是，通过 `$attach` | 否 |
| 调试 | 默认 REPL，与已调试的 Python 进程通信 | 标准编辑 | 仅调试 | 否 |
| IPython | REPL 与 IPython 后端通信 | IPython 命令，Pylab 的便利 | 否 | 是，在 REPL 中内联 |
| 带 Pylab 的 IPython | REPL 与 IPython 后端通信 | 标准 IPython | 否 | 是，单独窗口 |

本文介绍标准  REPL 模式和调试  REPL 模式。 有关 IPython 模式的详细信息，请参阅[使用 IPython REPL](interactive-repl-ipython.md)。

有关包含示例的详细演练，包括与编辑器的交互（如 Ctrl+Enter），请参阅[教程步骤 3   ：使用交互 REPL 窗口](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)。

## <a name="open-an-interactive-window"></a>打开交互窗口

以下有几种方法可用于针对某个环境打开交互  窗口。

方法一，切换到 Python 环境窗口（“视图”   > “其他窗口”   > “Python 环境”  或 Ctrl  +K   > Ctrl  +`  ），然后针对选定的环境，选择“打开交互窗口”  命令或按钮。

![Python 环境窗口中的交互窗口链接](media/interactive-window-opening.png)

方法二，在“视图”   > “其他窗口”  菜单底部附近，可以针对默认环境使用“Python 交互窗口”  命令，另外还有一个命令可用于切换到环境  窗口：

![“视图”>“其他窗口”中的交互窗口菜单项](media/interactive-window-menu.png)

方法三，可以通过选择“调试”   > “在 Python 交互窗口中执行 [项目 | 文件]”**Execute \<** 菜单命令 (Shift  +Alt  +F5  )，打开项目中启动文件的交互窗口，或独立文件的交互  窗口：

![在 Python 交互菜单中执行项目](media/interactive-execute-project.png)

最后，可以选中文件中的代码，然后如下所述，使用[发送到交互  命令](#send-to-interactive-command)。

## <a name="interactive-window-options"></a>交互窗口选项

可以通过“工具”   > “选项”   > “Python”   > “交互窗口”  控制“交互”  窗口的各个方面（请参阅[选项](python-support-options-and-settings-in-visual-studio.md)）：

![Python 交互窗口选项](media/options-interactive-windows.png)

## <a name="use-the-interactive-window"></a>使用交互窗口

交互  窗口打开后，可以在 \>\>\>  提示符处逐行输入代码。 交互  窗口会执行输入的每一行代码，包括导入模块、定义变量等：

![Python 交互窗口](media/interactive-window.png)

例外情况是需要其他行的代码才能补全语句，例如 `for` 语句以冒号结束，如上所示。 在这些情况下，行提示符将更改为 ...  ，指示需要输入程序块的其他行，如上图中的第四和第五行所示。 在空白行上按 Enter  键时，交互  窗口会关闭程序块，并在解释器中运行该程序块。

> [!Tip]
> 交互  窗口通过自动缩进属于周边范围的语句，改进常用 Python 命令行的 REPL 体验。 其历史记录（使用向上键重新调用）还提供多行项，而命令行 REPL 仅提供单行。

<a name="meta-commands"></a>交互  窗口还支持多个元命令。 所有元命令都以 `$` 开头，你可以键入 `$help` 获得元命令和 `$help <command>` 的列表，以获取特定命令的使用情况详细信息。

| 元命令 | 描述 |
| --- | --- |
| `$$` | 插入注释，用于注释会话中的代码。 |
| `$attach` | 将 Visual Studio 调试器附加到 REPL 窗口进程以启用调试。 |
| `$cls`，`$clear` | 清除编辑器窗口的内容，使历史记录和执行上下文保持不变。 |
| `$help` | 显示命令列表，或有关特定命令的帮助。 |
| `$load` | 从文件加载命令并执行，直到完成。 |
| `$mod` | 将当前范围切换为指定模块名称。 |
| `$reset` | 将执行环境重置为初始状态，但保留历史记录。 |
| `$wait` | 至少等待指定的毫秒数。 |

Visual Studio 扩展还可以通过实现和导出 `IInteractiveWindowCommand` 来扩展命令（[示例](https://github.com/Microsoft/PTVS/blob/master/Python/Product/PythonTools/PythonTools/Repl/InteractiveWindowCommands.cs#L85)）。

## <a name="switch-scopes"></a>切换范围

默认情况下，项目交互  窗口的范围为项目的启动文件，就像从命令提示符处运行一样。 对于独立文件，其范围为该文件。 但是，在 REPL 会话期间，可随时使用交互  窗口顶部的下拉列表菜单更改范围：

![交互窗口的范围](media/interactive-scopes.png)

导入模块后（如键入 `import importlib`），下拉列表中将显示可切换到该模块任意范围的选项。 交互  窗口中的消息还会指示新的范围，可用于跟踪会话期间如何达到某个特定状态。

在某个范围中输入 `dir()` 将显示该范围的有效标识符，包括函数名称、类和变量。 例如，使用 `import importlib` 后跟 `dir()` 将显示以下内容：

![Importlib 范围中的交互窗口](media/interactive-importlib-scope.png)

## <a name="send-to-interactive-command"></a>发送到交互命令

除了直接在交互  窗口中处理代码，还可以在编辑器中选中代码，单击右键，并选择“发送到交互”  ，或按 Ctrl  +Enter  。

![发送到交互式菜单命令](media/interactive-send-to.png)

此命令非常适用于迭代或演化代码开发，包括在开发时测试代码。 例如，将一段代码发送到交互  窗口并显示其输出后，可以按向上键再次显示代码、对其进行修改，并通过按 Ctrl  +Enter  快速测试。 （在输入结束时按 Enter  将执行它，但在输入过程中按 Enter  将插入新行。）如果有需要的代码，可以轻松将其复制回项目文件。

> [!Tip]
> Visual Studio 默认会删除 >>>  和 ...  将代码从交互  窗口粘贴到编辑器时，REPL 会发出提示。 可以在“工具”   > “选项”   > “文本编辑器”   > “Python”   > “高级”  选项卡上使用“粘贴删除 REPL 提示”  选项更改此行为。 请参阅[选项 - 杂项选项](python-support-options-and-settings-in-visual-studio.md#miscellaneous-options)。

<!-- After 15.3 is released, you can also press **Undo** after pasting to restore prompts. Press **Undo** a second time to remove the pasted code entirely. -->

## <a name="work-with-code-cells"></a>使用代码单元

代码单元可用于数据分析，并且受到各种文本编辑器支持。

例如，将代码文件用作暂存器时，通常有一小部分代码块需要一次性全部发送。 为了汇集代码，可以在单元开头添加以 `#%%` 开头的注释，将代码标记为代码单元，结束前一个代码单元  。 代码单元可以折叠和展开，在代码单元内使用 Ctrl  +Enter  会将整个单元发送到交互  窗口并移动到下一个代码单元。

Visual Studio 还会检测以 `# In[1]:` 等注释开头的代码单元，将 Jupyter 笔记本导出为 Python 文件时会获得这种格式。 通过此次检测，可以轻松地运行 [Azure Notebooks](https://notebooks.azure.com/) 的笔记本，只需下载为 Python 文件，在 Visual Studio 中打开并使用 Ctrl  +Enter  运行每个单元即可。

![交互式代码单元](media/interactive-code-cells.png)

## <a name="intellisense-behavior"></a>IntelliSense 的行为

与代码编辑器中 IntelliSense 仅基于源代码分析不同，交互  窗口中，IntelliSense 基于活动的对象。 这些建议在交互  窗口中更为正确，尤其是在使用动态生成代码的情况下。 缺点是具有副作用（如记录消息）的函数可能会影响开发体验。

如果此行为造成了困扰，请在“完成模式”  组的“工具”   > “选项”   > “Python”   > “交互窗口”  下更改设置，如[选项 - 交互窗口选项](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options)所述。
