---
title: Python 的选项和设置
description: Visual Studio 中与 Python 代码和项目相关的各种设置的引用。
ms.date: 03/13/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Python_Tools
- VS.ToolsOptionsPages.Python_Tools.General
- VS.ToolsOptionsPages.Python_Tools.Debugging
- VS.ToolsOptionsPages.Python_Tools.Diagnostics
- VS.ToolsOptionsPages.Python_Tools.Experimental
- VS.ToolsOptionsPages.Python_Tools.Interactive_Windows
- VS.ToolsOptionsPages.Text_Editor.Python.Advanced
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- python
- data-science
ms.openlocfilehash: 08501d71400a0df139022f04e68573d0dd1449d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89315130"
---
# <a name="options-for-python-in-visual-studio"></a>Visual Studio 中的 Python 选项

若要查看 Python 选项，请使用“工具”   > “选项”  菜单命令，确保选择“显示所有设置”  ，然后导航到“Python”  ：

::: moniker range="vs-2017"
![Python“选项”对话框，“常规”选项卡](media/options-general.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Python“选项”对话框，“常规”选项卡](media/options-general-2019.png)
::: moniker-end

在“文本编辑器”   > “Python”   > “高级”  选项卡上，以及在“文本编辑器”  组中的“环境”   > “字体和颜色”  选项卡上，还具有其他特定于 Python 的选项。

> [!Note]
> “实验”  组包含用于仍在开发中且未记录在本文中的功能的选项。 通常可在 [Microsoft 博客 Python 工程](https://devblogs.microsoft.com/python/)上的文章中找到其相关信息。

## <a name="general-options"></a>常规选项

（“工具”   > “选项”   > “Python”  选项卡。）

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **在创建虚拟环境时显示输出窗口**| On | 清除该选项可避免显示输出  窗口。 |
| **在安装或删除包时显示输出窗口** | On | 清除该选项可避免显示输出  窗口。 |
| **显示通知栏以创建环境** | On | *仅限 Visual Studio 2019。* 设置此选项并在用户打开包含 requirements.txt  或 environment.yml  文件的项目（而不是使用默认全局环境）时，Visual Studio 将显示包含分别创建虚拟环境或 conda 环境的建议的信息栏。 |
| **显示通知栏以安装包** | On | *仅限 Visual Studio 2019。* 设置此选项并在用户打开包含 requirements.txt  文件的项目（而不是使用默认全局环境）时，Visual Studio 会将这些要求与当前环境中安装的包进行比较。 如果缺少任何包，Visual Studio 会显示安装这些依赖项的提示。 |
| **始终以管理员身份运行包管理器** | Off | 始终为所有环境提升 `pip install` 和类似的包管理器操作。 安装包时，如果环境位于文件系统（如 c:\Program Files  ）的保护区域内，Visual Studio 将提示需要管理员权限。 出现该提示时，可选择始终仅为此环境提升 install 命令。 请参阅[“包”选项卡](python-environments-window-tab-reference.md#packages-tab)。 |
| **初次使用时自动生成完成 DB** | On | *应用 Visual Studio 2017 版本 15.5 和早期版本，并在使用 IntelliSense 数据库时应用更高版本。* 在编写使用某个库的代码时，优先完成此库的数据库。 有关详细信息，请参阅 [IntelliSense 选项卡](python-environments-window-tab-reference.md?view=vs-2017#intellisense-tab)。 |
| **忽略系统级 PYTHONPATH 变量** | On | 默认情况下会忽略 PYTHONPATH，因为 Visual Studio 提供了一种更直接的方式来指定环境和项目中的搜索路径。 请参阅[搜索路径](search-paths.md)了解详细信息。 |
| **添加链接文件时更新搜索路径** | On | 如果已设置此选项，将一个[链接文件](managing-python-projects-in-visual-studio.md#linked-files)添加到项目会更新[搜索路径](search-paths.md)，以便 IntelliSense 能在其完成数据库中包含链接文件的文件夹的内容。 清除此选项将从完成数据库中排除此类内容。 |
| **在找不到导入模块时发出警告** | On | 当知道导入模块当前不可用但不会影响代码操作时，清除此选项可禁止发出警告。 |
| **将缩进不一致报告为** | **警告** | 由于 Python 解释器严重依赖于正确的缩进来确定作用域，因此默认情况下，Visual Studio 将在检测到可能指示编码错误的缩进不一致时发出警告。 设置为“错误”可提升严格度，这样会导致出现这些情况时退出程序  。 若要完全禁用此行为，请选择“不”  。 |
| **检查调查/新闻** | **每周一次** | *Visual Studio 2017 及更早版本。* 设置频率，允许 Visual Studio 以此频率打开窗口，此窗口包含一个网页，其中含有 Python 相关的调查和新闻条目（如果有）。 选项包括“从不”、“每天一次”、“每周一次”和“每月一次”     。 |
| **重置所有永久隐藏的对话框**（按钮） | n/a | 各对话框提供“不再显示”等选项  。 使用此按钮可清除这些选项并重新显示对话框。 |

::: moniker range="vs-2017"
![Python“选项”对话框，“常规”选项卡](media/options-general.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Python“选项”对话框，“常规”选项卡](media/options-general-2019.png)
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="conda-options"></a>Conda 选项

（“工具”>“选项”>“Python”>“Conda”选项卡。     ）

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **Conda 可执行文件路径** | (空白) | 指定 conda.exe  可执行文件的准确路径，而不是依赖于 Python 工作负载随附的默认 Miniconda 安装。 如果此处提供了其他路径，则会优先于默认安装和注册表中指定的任何其他 conda.exe 可执行文件。 如果手动安装较新版本的 Anaconda 或 Miniconda，或者想要使用 32 位发行版（而不是默认 64 位发行版），则可能会更改此设置。 |

![“Python 选项”对话框，“语言服务器”选项卡](media/options-conda.png)

::: moniker-end

## <a name="debugging-options"></a>调试选项

（“工具”   > “选项”   > “Python”   > “调试”  选项卡。）

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **当存在错误时，在运行前发出提示** | On | 如果设置此选项，系统会提示是否确定要运行包含错误的代码。 清除此选项将禁用警告。 |
| **在进程异常退出时等待输入**<br/><br/>**在进程正常退出时等待输入** | On（两者皆是） | 通过 Visual Studio 启动的 Python 程序在其自己的控制台窗口中运行。 默认情况下，无论程序如何退出，窗口都会等待用户按键才会关闭。 若要删除提示并自动关闭窗口，请清除其中任一选项或全部清除。 |
| **让程序输出显示在“调试输出”窗口** | On | 同时在一个单独的控制台窗口和 Visual Studio 输出  窗口中显示程序输出。 清除此选项可仅在单独控制台窗口中显示输出。 |
| **在出现 SystemExit 异常（退出代码为 0）时中断** | Off | 如果设置此选项，将在出现此异常时停止调试器。 清除后，调试器将退出，但不会中断。 |
| **启动 Python 标准库调试** | Off | 可支持在调试时逐步执行标准库源代码，但会增加调试器启动的时间。|
| **显示函数返回值** | On | *仅限 Visual Studio 2019。* 显示“局部变量”  窗口中的函数返回值，然后转到调试程序中的函数调用 (F10) |
| **使用旧版调试程序** | Off | *仅限 Visual Studio 2019。* 指示 Visual Studio 默认使用旧版调试程序。 有关详细信息，请参阅[调试 - 使用旧版调试程序](debugging-python-in-visual-studio.md#use-the-legacy-debugger)。 |

::: moniker range="vs-2017"
![Python“选项”对话框，“调试”选项卡](media/options-debugging.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Python“选项”对话框，“调试”选项卡](media/options-debugging-2019.png)
::: moniker-end

## <a name="diagnostics-options"></a>诊断选项

（“工具”   > “选项”   > “Python”   > “诊断”  选项卡。）

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **包含分析日志** | On | 在使用按钮将诊断保存到文件或将其复制到剪贴板时，包含与已安装 Python 环境分析相关的详细日志。 此选项可能会显著增加所生成文件的大小，但诊断 IntelliSense 问题时通常需要使用此选项。 |
| **将诊断保存到文件**（按钮） | n/a | 提示输入文件名，然后将日志保存到文本文件。 |
| **将诊断复制到剪贴板**（按钮） | n/a | 将整个日志放到剪贴板上；此操作可能需要一些时间，具体取决于日志的大小。 |

![Python“选项”对话框，“诊断”选项卡](media/options-diagnostics.png)

## <a name="interactive-windows-options"></a>交互窗口选项

（“工具”   > “选项”   > “Python”   > “交互窗口”  选项卡。）

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **脚本** | n/a | 指定启动脚本的常规文件夹，将其应用于所有环境的交互  窗口。 请参阅[启动脚本](python-environments-window-tab-reference.md#startup-scripts)。 但请注意，此功能当前无效。 |
| **向上/向下箭头浏览历史记录** | On | 使用箭头键在交互  窗口中浏览历史记录。 清除此设置可改为使用箭头键在交互  窗口的输出中浏览。 |
| **完成模式** | **仅计算不包含函数调用的表达式** | 要确定交互  窗口中表达式上的可用成员，可能需要评估当前未完成的表达式，这可能带来负作用或导致多次调用函数。 “仅评估表达式而无需调用函数”是默认设置，此设置可排除可能调用函数的表达式，并对其他表达式进行评估  。 例如，会评估 `a.b`，但不会评估 `a().b`。  “永不评估表达式”仅使用常规 IntelliSense 引擎获取建议，可避免所有副作用  。 “评估所有表达式”会评估完整的表达式以获取建议，不考虑是否存在副作用  。 |
| **隐藏静态分析建议** | Off | 如果设置此选项，将仅显示通过评估表达式获取的建议。 如果与完成模式  的值“永不评估表达式”  结合使用，交互  窗口中将不会显示任何有用的完成。 |

![Python“选项”对话框，“交互窗口”选项卡](media/options-interactive-windows.png)

::: moniker range=">=vs-2019"
## <a name="language-server-options"></a>语言服务器选项

（“工具”>“选项”>“Python”>“语言服务器”选项卡。     ）

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **从 Typeshed 禁用完成** | Off | Visual Studio IntelliSense 通常使用捆绑版本的 Typeshed（一组 .pyi  文件）来查找 Python 2 和 Python 3 的标准库和第三方库的类型提示。 设置此选项将禁用捆绑的 TypeShed 行为。 |
| **自定义 Typeshed 路径** | (空白) | 如果已设置，则 Visual Studio 会在此路径（而不是其捆绑版本）中使用 Typeshed 文件。 如果已设置“从 Typeshed 禁用完成”  ，则忽略。 |

![“Python 选项”对话框，“语言服务器”选项卡](media/options-language-server.png)

::: moniker-end

## <a name="advanced-python-editor-options"></a>高级 Python 编辑器选项

（“工具”   > “选项”   > “文本编辑器”   > “Python”   > “高级”  选项卡。）

### <a name="completion-results"></a>完成结果

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **成员完成显示成员的交集** | Off | 如果设置此选项，将仅显示所有可能类型支持的完成。 |
| **基于搜索字符串筛选列表** | On | 在键入时，对完成建议应用筛选（默认选中）。 |
| **为所有标识符自动显示完成项** | On | 清除此选项将同时在编辑器和交互  窗口中禁用完成。 |

### <a name="selection-in-completion-list"></a>完成列表中的选定内容

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **通过键入以下字符提交** | **{}\[\]().,:;+-*/%&&#124;^~=<>#@\\** | 这些字符通常位于可能是从完成列表中选取的标识符后面，因此只需键入字符即可轻松提交完成。 可根据需要在列表中删除或添加特定字符。  |
| **按 Enter 提交当前完成** | On | 如果设置此选项，按 Enter  键将选择并应用当前选择的完成（和上面的字符一样）（但由于没有针对 Enter  的字符，因此它无法直接进入该列表！）。 |
| **在完整键入的字末尾按 Enter 添加新行** | Off | 默认情况下，如果键入完成弹出窗口中显示的完整字词，然后按 Enter  ，则会提交该完成。 通过设置此选项，可在键入完标识符后有效提交完成，然后按 Enter  键即可插入新行。 |

### <a name="miscellaneous-options"></a>“杂项”选项

| 选项 | 默认 | 描述 |
| --- | --- | --- |
| **打开文件时进入大纲模式** | On | 打开 Python 代码文件时，自动在编辑器中打开 Visual Studio 的大纲显示功能。 |
| **粘贴已删除的 REPL 提示符** | On | 删除粘贴文本中的 >>>  和 ...  ，可从交互  窗口向编辑器轻松传输代码。 可根据需要清除此选项，以保留从其他源粘贴的字符。 |
| **基于类型为名称着色** | On | 在 Python 代码中启用语法着色。 |

![Python 编辑器“选项”对话框，“高级”选项卡](media/options-editor-advanced.png)

## <a name="fonts-and-colors-options"></a>“字体”和“颜色”选项

（“文本编辑器”  组中的“环境”   > “字体和颜色”  选项卡。）

Python 选项的名称都带有“Python”  前缀，且一目了然。 所有 Visual Studio 颜色主题的默认字体都为 10pt Consolas 常规体（不以粗体显示）。 默认颜色因主题而异。 通常情况下，当你在默认的字体或颜色设置下难以阅读文本时，你会对字体或颜色进行更改。

![Python 字体和颜色选项](media/options-fonts-and-colors.png)
