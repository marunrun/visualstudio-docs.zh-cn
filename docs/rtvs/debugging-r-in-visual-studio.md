---
title: 调试 R 代码
description: Visual Studio 为 R 提供完整的调试体验，包括断点、附加、调用堆栈和检查变量。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 98dcbaaeb6f330cda3a14cf8c32afe403b50aa85
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939260"
---
# <a name="debug-r-in-visual-studio"></a>在 Visual Studio 中调试 R

针对 Visual Studio 的 R 工具 (RTVS) 集成了 Visual Studio 的完整调试体验（请参阅[在 Visual Studio 中进行调试](/visualstudio/debugger/debugger-feature-tour)）。 此支持包括断点、附加到运行进程、检查和监视变量以及检查调用堆栈。 本文随后探讨了 R 和 RTVS 独有的调试特性性。

在 R 项目中启动 R 启动文件的调试器与启动其他项目类型的调试器相同：使用“调试” > “启动调试”、按 F5 键，或选择调试工具栏上的“源化启动文件”：

![R 的调试器启动按钮](media/debugger-start-button.png)

要更改启动文件，请右键单击解决方案资源管理器中的文件，并选择“设置为启动 R 脚本”。

在所有情况下，启动调试器都会在交互窗口中“源化”文件，这意味在该处加载并运行文件，如交互窗口的输出中所示：

```output
> rtvs::debug_source("c:/proj/rproject1/rproject1/script.R")
Sourcing: c:\proj\rproject1\rproject1\script.R
Sourcing: c:\proj\rproject1\rproject1\Settings.R
```

请注意，`rtvs::debug_source` 函数用于获取脚本。 此函数是必需的，因为 RTVS 需要修改代码，为调试做准备。 使用 RTVS 源命令并且已附加调试器时，Visual Studio 将自动使用 `rtvs::debug_source`。

也可使用“R 工具” > “会话” > “附加调试器”命令、“调试” > “附加到 R 交互”命令，或者交互窗口工具栏中的“附加调试器”命令，直接从交互窗口手动附加调试器。 进行此操作后，需要由你来源化要调试的文件。 如果要手动获取文件，请确保使用 `rtvs::debug_source` 而非 R 中的常规 `source` 命令。

调试器与交互窗口之间的此连接简化了使用不同参数值调用（和调试）函数等操作。 例如，假设（从某个源）获得的文件（意味着文件已加载到会话中）中有如下函数：

```R
add <- function(x, y) {
    return(x + y)
}
```

然后，在 `return` 语句中设置一个断点。 现在在交互式窗口中，可输入 `add(4,5)` 使调试器在断点处停止。

## <a name="environment-browser-in-the-interactive-window"></a>交互窗口中的环境浏览器

在调试器中停止时，还会在[交互窗口](interactive-repl-for-r-in-visual-studio.md)中的环境浏览器提示符处停止。 提示符显示为 `Browse[n]>`，其中 n 是一个数字。

环境浏览器支持若干特殊命令：

| 命令 | 说明 |
| --- | --- |
| n | 下一个：运行代码文件中的下一个语句（与逐步执行相同）。 |
| 秒 | 单步执行：运行代码文件中的下一个语句，如果下个一语句是函数调用，则单步执行函数范围。 |
| f | 完成：运行当前函数范围的剩余部分，并返回到调用方（与跳出相同）。 |
| c, cont | 继续：运行程序，直至到达下一个断点。 |
| Q | 退出：结束调试会话。 |
| 其中 | 显示堆栈：在交互窗口中显示调用堆栈。 |
| 帮助 | 显示帮助：在交互窗口中显示可用命令。 |
| &lt;expr&gt; | 在 expr 中计算表达式。 |

![交互窗口中的环境浏览器](media/debugger-environment-browser.png)
