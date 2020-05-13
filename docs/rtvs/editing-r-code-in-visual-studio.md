---
title: 编辑 R 代码
description: Visual Studio 为 R 提供量身定制的编辑体验，同时保留所有功能并且能够使用扩展。
ms.date: 11/05/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 7ecfd8f1cf50e94991ce2fd94ad94ac9815c92ca
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307069"
---
# <a name="edit-r-code-in-visual-studio"></a>在 Visual Studio 中编辑 R 代码

针对 Visual Studio 的 R 工具 (RTVS) 为 R 专门量身定制 Visual Studio 编辑体验，同时保留所有功能并且能够使用扩展。 （例如，如果偏好 VIM 键绑定，可从 Visual Studio Marketplace 安装免费的 [VsVim 扩展](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim)。）

除了本文中的功能，另请参阅 [IntelliSense](r-intellisense.md)、[linting](linting-r-code.md)、[代码片段](code-snippets-for-r.md)和 [R Markdown](rmarkdown-with-r-in-visual-studio.md)。

## <a name="syntax-highlighting"></a>语法突出显示

除通过颜色区分不同的代码部分（如字符串、注释和关键字），RTVS 还可以在注释中突出显示和启用链接：

![R 代码的语法着色](media/editing-syntax-colors.png)

要自定义字体和某些突出显示颜色，请选择“工具” > “选项”命令，导航到“环境” > “字体和颜色”，然后在“显示项:”框中更改与 R 相关的项的设置      ：

![R 代码的字体和颜色选项](media/editing-syntax-colors-options.png)

Visual Studio 同时还用下划线标出编辑器中的语法错误：

![R 代码中的语法错误突出显示](media/editing-syntax-error.png)

要更改此行为，请查看“[编辑器选项](#editor-options)”下的“高级”   > “语法检查”设置  。

## <a name="edit-and-organize-code"></a>编辑和整理代码

键入代码时，RTVS 将提供 [IntelliSense](r-intellisense.md) 页中所述的自动补全功能。 它还将设置自动格式，如大括号和括号补全：

![内联格式设置动画](media/editing-inline-formatting.gif)

当键入对具有多个参数的函数的调用时，通常希望将这些参数排成一列，以方便阅读代码。 RTVS 会记住为参数设置的缩进，并将其自动应用于后续行：

![自动缩进动画](media/editing-auto-indentation.gif)

若要更改此行为，请查看 **“选项卡”** 组的 [“编辑器选项”](#editor-options)。

通过可折叠代码区域，可以在编辑器中暂时隐藏部分代码。 对于多行语句，除非“高级” > “大纲显示” > “代码大纲显示”选项设为“关闭”，否则 Visual Studio 将自动创建多个区域    。

要创建自己的区域，请在所需代码周围添加以 `---` 结尾的注释。 通过代码左侧的小型 +/- 控件可以展开或折叠区域：

![创建含注释的可折叠区域](media/editing-collapsible-regions.gif)

默认情况下，按下 Tab 键时 Visual Studio 将插入空格  。 可以按[操作、文本编辑器、选项卡](../ide/reference/options-text-editor-all-languages.md)中所述再次更改此行为。

## <a name="code-navigation"></a>代码导航

通过代码导航可以快速访问 R 程序及其库的源代码。 通过这些功能可以专注于工作，而不必手动搜索代码。

通过“转到定义”可快速跳到函数定义，或弹出一个内联微型编辑器，用于读取库函数的源代码  。 只需右键单击感兴趣的函数，选择“转到定义”  ，或将游标置于函数中并按 F12  。

此命令将打开一个新编辑器窗口，其中包含该函数的源代码。 游标位于函数定义的开头，非常方便。

“速览定义”  通过右键单击菜单或按 Alt+F12 调用，在函数调用的下方插入包含函数源代码的只读、可滚动区域   ：

![速览定义动画](media/editing-peek-definition.gif)

## <a name="send-code-to-the-interactive-window"></a>将代码发送到交互窗口

许多开发人员喜欢在编辑器中编写代码，然后将代码发送到[交互窗口](interactive-repl-for-r-in-visual-studio.md)立即测试（也被称为读取-评估-输出-循环或 REPL）。 在 R 编辑器中按 Ctrl  +Enter  可以将当前行的代码发送到交互式窗口，然后游标将移到下一行。 按 Ctrl  +Enter  ，然后可在编辑器中有效地单步执行代码。

也可选择代码，按 Ctrl  +Enter  应用全部所选内容。 或者右键单击选择部分，然后选择“交互执行”  。

## <a name="format-code"></a>格式代码

Visual Studio 自动格式设置按照首选项中的设置，设置写入的代码以及粘贴到编辑器的代码的格式。 也可以通过选择，右键单击，选择“格式选择”  （Ctrl  +K、F   ）以应用这些首选项。 例如，如果所有函数定义都在一行中：

```R
f<-function  (a){  return(a + 1) }
```

应用格式将它整理为：

```R
f <- function(a) { return(a + 1) }
```

若要重格式化整个代码文件：请选择“编辑” > “高级” > “设置文档的格式”  （Ctrl+E、D）      。

自动格式设置是可以撤消的单独操作。 例如，如果将代码及其应用的格式粘贴到编辑器，选择“编辑” > “撤消”或按一次 Ctrl+Z 将撤消格式设置；按第二次“撤消”将撤消粘贴操作      。

通过“文本编辑器” > “R” > “高级”选项卡上的“工具” > “选项”可设置格式选项（包括关闭格式设置）      。    可以使用“R 工具” > “编辑器选项”命令，或通过在编辑器中右键单击并选择“格式设置选项”直接转到此页面。 请参阅[编辑器选项](#editor-options)部分了解详细信息。

## <a name="inserting-roxygen-comments"></a>插入 Roxygen 注释

RTVS 提供一种快捷方式，通过使用函数的参数名来生成 [Roxygen](https://cran.r-project.org/web/packages/roxygen2/index.html) 注释。 只需在函数定义上方的空白行中键入 `###`：

![插入 Roxygen 注释动画](media/editing-roxygen-comments.gif)

## <a name="editor-options"></a>编辑器选项

通过“工具” > “选项”命令导航到“文本编辑器” > “R”，或使用快捷方式命令“R 工具” > “编辑器选项”来设置特定于编辑器的选项       。

“常规”  、“滚动条”  和“选项卡”  选项卡中的选项并非特定于 R，而是相当常见的 Visual Studio 设置，可用于所有语言，但要根据每种语言来应用。 有关详细信息，请参阅以下文章：

- [“选项”->“文本编辑器”->“所有语言”](../ide/reference/options-text-editor-all-languages.md)
- [通过自定义滚动条来跟踪代码](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)
- [选项、文本编辑器和选项卡](../ide/reference/options-text-editor-all-languages-tabs.md)

“R” >   “高级”  选项卡上的选项特定于 RTVS：

| Group | 选项 | 默认 | 描述 |
| --- | --- | --- | --- |
| 格式化 | 自动格式设置 | On | 在键入时重格式化代码。 不影响“设置选定内容的格式”  或“设置文档的格式”  命令。 |
| | 扩展大括号 | Off | 将左大括号 { 置于新行。 |
| | 粘贴时设置格式 | On | 粘贴时应用格式设置。 |
| | 设置 } 范围的格式 | On | 设置键入右大括号 } 后的范围的格式。 |
| | 逗号后空格 | On | 在逗号后添加空格。 |
| | 关键字后空格 | On | 在 `if`、`while` 和 `repeat` 之类的关键字后添加空格。 |
| | { 之前空格 | On | 在左大括号 { 之前添加空格。 |
| | = 左右空格 | On | 在等号左右添加空格。 |
| IntelliSense | Enter 键提交 | Off | 按下 Enter 后提交自动补全选择  。 |
| | 空格键提交 | Off | 按下空格键后提交自动补全选择  。|
| | 第一个字符显示补全列表 | On | 键入第一个字符时显示补全列表。 关闭时，通过“编辑” >   “IntelliSense” >    “列表成员”  (Ctrl+J) 来显示补全列表  。 |
| | Tab 键调用补全列表  | Off | 键入一个或多个字符并按 Tab 来调用补全列表  。 |
| | 匹配部分输入参数名 | Off | 在函数调用中键入参数名时，签名帮助显示最佳匹配的参数说明。 |
| 交互窗口 | 在 R 控制台中进行语法检查 | Off | 在交互窗口中应用语法检测。 在多行语句中，语法检查可能无法正常工作。 |
| 大纲显示 | 代码大纲显示 | On | 为多行语句这样的区域自动创建可折叠区域。 |
| 语法检查 | 显示语法错误 | On | 为代码启用自动语法检查。 |
