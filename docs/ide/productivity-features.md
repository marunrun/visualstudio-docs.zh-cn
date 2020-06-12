---
title: 实用指南
ms.date: 4/29/2020
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33eb146ce36bfa36dbe28fdcec0f7dfb85daa59b
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184076"
---
# <a name="productivity-guide-for-visual-studio"></a>Visual Studio 实用指南

如果想要在编写代码时节省时间，请阅读本指南。 本实用指南包含一些技巧，可帮助你开始使用 Visual Studio、编写代码、调试代码、处理错误，以及使用键盘快捷方式 - 所有这些内容都在一页中提供。

有关有用的键盘快捷方式的信息，请参阅[工作效率快捷方式](../ide/productivity-shortcuts.md)。 有关命令快捷方式的完整列表，请参阅[默认键盘快捷方式](../ide/default-keyboard-shortcuts-in-visual-studio.md)。

## <a name="get-started"></a>入门

你可以通过快速搜索所需的任何内容（包括命令、设置、文档和安装选项）来节省在菜单中进行探索的时间。 请在 Visual Studio 的搜索结果中查看命令的键盘快捷方式，以便更轻松记住它们。 

- **使用任务列表模拟代码**。 如果没有足够的请求来完成某个代码段，请使用“任务列表”跟踪使用 `TODO` 和 `HACK` 令牌或自定义令牌的代码注释，并管理直接导向代码中预定义位置的快捷方式。 有关详细信息，请参阅[使用任务列表](../ide/using-the-task-list.md.)。

- **使用解决方案资源管理器快捷方式**。 如果你不熟悉 Visual Studio，这些快捷方式将派上用场，能够在你加快新代码库的速度时为你节省时间。 有关快捷方式的完整列表，请参阅 [Visual Studio 中的默认键盘快捷方式](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solutionexplorerGLOBAL)。

- [在 Visual Studio 中识别并自定义键盘快捷方式](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。 你可以认识 Visual Studio 命令的键盘快捷键，自定义这些快捷键并将其导出以供他人使用。 你可以在“选项”对话框中找到并更改键盘快捷方式。

- **使 Visual Studio 更易于访问**。 Visual Studio 具有内置辅助功能，这些辅助功能与屏幕阅读器以及其他辅助技术兼容。 有关可用功能的完整列表，请参阅 [Visual Studio 的辅助功能提示和技巧](../ide/reference/accessibility-tips-and-tricks.md)。 

- **查看 Visual Studio 产品生命周期和维护**。 要了解如何获取 Visual Studio 更新、适用于企业和专业客户的支持选项、对旧版 Visual Studio 的支持以及 Visual Studio 维护未包含的组件，请参阅 [Visual Studio 产品生命周期和维护](https://docs.microsoft.com/visualstudio/releases/2019/servicing)。 

- **在 Visual Studio 中安装和管理 NuGet 包**。 通过 Windows 版 Visual Studio 中的 NuGet 包管理器 UI，可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。 有关详细信息，请参阅[使用 NuGet 包管理器在 Visual Studio 中安装和管理包](https://docs.microsoft.com/nuget/consume-packages/install-use-packages-visual-studio)。

## <a name="write-code"></a>编写代码

使用以下功能快速编写代码。

- **使用便捷命令**。 Visual Studio 提供各种有助于更快速完成常见编辑任务的命令。 例如，选择一个命令，即可轻松复制代码行，而无需复制它、重新定位光标并粘贴它。 依次选择“编辑” > “复制”，或按 Ctrl+E、V。 此外，还可以通过选择“编辑” > “高级” > “展开选定内容”或“编辑” > “高级” > “合拢选定内容”，或按“Shift”+“Alt”+“=”或“Shift”+“Alt”+“-”，快速展开或合拢选定文本内容            。

- **使用 IntelliSense**。 在编辑器中输入代码时，将会显示 IntelliSense 信息，如列表成员、参数信息、快速信息，签名帮助和完整单词。 这些功能支持文本的模糊匹配；例如，列表成员的结果列表不仅包括以你输入的字符开头的条目，还包括在名称的任何位置包含字符组合的条目。 有关详细信息，请参阅[使用 IntelliSense](../ide/using-intellisense.md)。

- **输入代码时，更改 IntelliSense 选项的自动插入**。 通过将 IntelliSense 切换到建议模式，可以指定只有显式选中时才插入 IntelliSense 选项。

     若要启用建议模式，请按 Ctrl+Alt+空格键键，也可以在菜单栏上依次选择“编辑” > “IntelliSense” > “切换完成模式”。

- **使用代码片段**。 可以使用内置代码片段，也可以创建自己的代码片段。

     若要插入代码片段，请在菜单栏上依次选择“编辑” > “IntelliSense” > “插入代码片段”或“包围方式”，也可以打开文件中的快捷菜单，并依次选择“代码片段” > “插入代码片段”或“包围方式”。 有关详细信息，请参阅[代码片段](../ide/code-snippets.md)。

- **修复内联代码错误**。 通过快速操作，只凭单个操作便可轻松重构、生成或修改代码。 可使用螺丝刀![螺丝刀图标](media/screwdriver-icon.png)或灯泡![灯泡图标](media/light-bulb-icon.png)图标，或按“Alt”+“Enter”或“Ctrl”应用这些操作。+ 前提是光标位于相应的代码行上。 有关详细信息，请参阅[快速操作](quick-actions.md)。

- **显示并编辑代码元素的定义**。 你可以快速显示和编辑定义代码元素（如成员、变量或局部变量）的模块。

    若要在弹出窗口中打开定义，请选中元素，再按 Alt+F12 键，也可以打开元素的快捷菜单，再选择“速览定义”。 若要在单独的代码窗口中打开定义，请打开元素的快捷菜单，然后选择“转到定义”。

- **使用示例应用程序**。 可通过从 [Microsoft Developer Network](https://code.msdn.microsoft.com/) 下载并安装示例应用程序来加速应用程序的开发。 还可以通过下载并探索相关领域的示例包学习特定的技术或编程概念。

- **使用格式设置/换行更改大括号格式**。 通过“格式设置”选项页面，可在代码编辑器中设定代码格式设置选项，其中包括换行。 有关如何在 C# 中使用此设置的详细信息，请参阅[“选项”对话框：“文本编辑器”>“C#”>“代码样式”>“格式设置”](../ide/reference/options-text-editor-csharp-formatting.md)。 对于 C++，请参阅[在 Visual Studio 中设置 C++ 代码首选项](https://docs.microsoft.com/cpp/ide/how-to-set-preferences)。 对于 Python，请参阅[设置 Python 代码格式](../python/formatting-python-code.md)。

- **使用制表符更改缩进**。 使用自定义编辑器设置（专为每个代码库定制）对在不同编辑器和 IDE 中处理同一项目的多个开发人员强制实施一致的编码样式。 确保整个团队遵循相同的语言约定、命名约定和格式设置规则。 由于这些自定义设置是可移植的，可随代码移动，因此即使在 Visual Studio 外部也可以强制执行编码样式。 有关详细信息，请参阅[选项、文本编辑器、所有语言、制表符](../ide/reference/options-text-editor-all-languages-tabs.md#tabs)。

## <a name="navigate-within-your-code-and-the-ide"></a>在代码和 IDE 中导航

你可以使用各种技术更快地查找并移动到代码中的特定位置。 你还可以根据偏好更改 Visual Studio 窗口的布局。 

- **为代码行添加书签**。 你可以使用书签来快速浏览到文件中的特定代码行。

    若要设置书签，请在菜单栏上依次选择“编辑” > “书签” > “切换书签”。 可以在“书签”窗口中查看解决方案的所有书签。 有关详细信息，请参阅[在代码中设置书签](../ide/setting-bookmarks-in-code.md)。

- **在文件中搜索符号定义**。 可在解决方案内进行搜索以查找符号定义和文件名，但搜索结果不包含命名空间或局部变量。

   若要访问此功能，请在菜单栏上依次选择“编辑” > “转到”。

- **浏览代码的整体结构**。 在“解决方案资源管理器”中，可以搜索并浏览项目中的类及其类型和成员。 还可以搜索符号，查看方法的调用层次结构，查找符号引用，以及执行其他任务。 如果在“解决方案资源管理器”中选择一个代码元素，则在“预览”选项卡中打开关联的文件，并且游标移至文件中的该元素。  有关详细信息，请参阅[查看代码的结构](../ide/viewing-the-structure-of-code.md)。

- **使用地图模式跳转到文件中的位置**。 地图模式在滚动条上以缩图形式显示代码行。 有关此显示模式的详细信息，请参阅[如何：自定义滚动条](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md#map-mode)。

- **通过代码图了解代码结构**。 代码图可帮助你可视化代码中的依赖项，并了解它们如何搭配使用，而无需读取文件和代码行。 有关详细信息，请参阅[映射代码图中的依赖项](../modeling/map-dependencies-across-your-solutions.md)。

- **使用“编辑/转到最近文件”查看经常使用的文件**。 使用 Visual Studio 中的“转到”命令执行代码的重点搜索，以帮助快速找到指定项。 有关详细说明，请参阅[使用“转到”命令查找代码](../ide/go-to.md)。

- **将[属性窗口](../ide/reference/properties-window.md)移到右侧**。 如果正在寻找更熟悉的窗口布局，则可通过按 F4 在 Visual Studio 中移动“属性”窗口。

## <a name="find-items-faster"></a>更快速查找项

你可以在 IDE 中搜索命令、文件和选项，还可以筛选工具窗口的内容以仅显示当前任务的相关信息。

- **筛选工具窗口的内容**。 可以搜索很多工具窗口（如“工具箱”、“属性”窗口以及“解决方案资源管理器”）的内容，但仅显示名称中包含指定的字符的项。  

- **仅显示要解决的错误**。 如果选中在“错误列表”工具栏中的“筛选器”按钮，则可减少出现在“错误列表”窗口中的错误数。   您只能显示在编辑器中打开的文件中的错误、当前文件中的错误，或者当前项目中的错误。 您还可以在“错误列表”窗口中进行搜索，以查找特定错误。

- **查找对话框、菜单命令、选项及更多内容**。 在搜索框中，输入想查找的项的关键字或词组。 例如，如果输入“新建项目”，则会出现以下选项：

   ::: moniker range="vs-2017"

   ![“新建项目”的快速启动结果](../ide/media/productivity_quicklaunch.png)

   “快速启动”显示创建新项目、将新项添加到项目、“选项”对话框中的“项目和解决方案”页的链接以及其他内容  。 搜索结果还可包括项目文件和工具窗口。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![“新建项目”的搜索结果](../ide/media/vs-2019/productivity-quick-launch-new-project.png)

   ::: moniker-end

   按 Ctrl+Q  可直接跳转至搜索框。

## <a name="debug-code"></a>调试代码

调试会消耗大量的时间，但以下提示将有助于加快这个过程。

- **使用 Visual Studio 调试器工具**。 在 Visual Studio 上下文中，当调试应用时，这通常意味着你在调试器模式下运行应用程序。 调试器在运行过程中可提供许多方法让你查看代码的情况。 有关入门指南，请参阅[初步了解 Visual Studio 调试器](../debugger/debugger-feature-tour.md)。 

- **在不同的浏览器中测试相同的页、应用程序或站点**。 在调试代码时，可在安装的 Web 浏览器（包括 [Page Inspector (Visual Studio)](https://msdn.microsoft.com/Library/65880969-1ad2-47be-85b9-bb12c81bf209)）之间轻松进行切换，而无需打开“浏览方式”对话框。 可使用“调试目标”列表（位于“标准”工具栏中的“启动调试”按钮旁）来快速验证在调试或查看页面时使用的浏览器  。

    ![选择 Web 浏览器调试选项](../ide/media/webbrowserdropdowntoolbar.png)

- **设置临时断点**。 你可以在当前代码行中创建一个临时断点，同时启动调试器。 点击该行代码时，调试器进入中断模式。 有关详细信息，请参阅[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。

    若要使用此功能，请选择 Ctrl+F10 键，或打开要中断的代码行的快捷菜单，然后选择“运行到游标处”。  

- **在调试过程中移动执行点**。 你可以将当前执行点移至代码的其他部分，然后从该点重新开始调试。 如果要调试一部分代码而不想重新创建到达这部分代码所需的所有步骤，此方法相当有效。 有关详细信息，请参阅[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。

     若要移动执行点，请将黄色箭头拖到同一源文件中希望设置下一条语句的位置，然后选择 F5 键继续调试。

- **获取变量的值信息**。 可以将数据提示添加至代码中的一个变量并将其固定，以便在调试完成后访问该变量的上一个已知值。 有关详细信息，请参阅[查看数据提示中的数据值](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)。

     若要添加数据提示，调试器必须处于中断模式。 将光标放在该变量上，然后在显示的数据提示中选择固定按钮。 调试停止时，源文件中包含该变量的代码行的旁边会显示蓝色图钉图标。 如果您指向蓝色图钉，则会显示最新调试会话中的变量的值。

- **清除即时窗口**。 可在设计时输入 `>cls` 或 `>Edit.ClearAll` 来清除[即时窗口](../ide/reference/immediate-window.md)的内容

     有关其他命令的详细信息，请参阅 [Visual Studio 命令别名](../ide/reference/visual-studio-command-aliases.md)。

- **[使用 CodeLens 查找代码更改和其他历史记录](../ide/find-code-changes-and-other-history-with-codelens.md)** 。 通过 CodeLens，你可以在专注于工作的同时了解代码所发生的情况 &mdash; 而无需离开编辑器。 可以查找代码引用、代码更改、关联的 Bug、工作项、代码评审和单元测试。

- **使用 Live Share 与其他人一起实时调试**。 使用 Live Share，无论使用什么编程语言、要生成哪种类型的应用，均可以与他人实时协作进行编辑和调试。 有关详细信息，请参阅[什么是 Visual Studio Live Share？](https://docs.microsoft.com/visualstudio/liveshare/)

- **使用交互窗口来编写和测试小型代码**。 Visual Studio 提供了一个读取-求值-打印循环 (REPL) 交互窗口，你可以在该窗口输入任意代码并查看即时结果。 这种编码方式有助于你了解与实验 API 和库，并以交互方式开发要包含在项目中的工作代码。 对于 Python，请参阅[使用 Python 交互窗口](../python/python-interactive-repl-in-visual-studio.md)。 此交互窗口功能还可用于 C#。 

## <a name="access-visual-studio-tools"></a>访问 Visual Studio 工具

如果将开发人员命令提示符或其他 Visual Studio 工具固定到“开始”菜单或任务栏，可以快速访问这些对象。

::: moniker range="vs-2017"

1. 在 Windows Explorer 中。浏览到 %ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2017\Visual Studio Tools。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Windows Explorer 中。浏览到 %ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2019\Visual Studio Tools。

::: moniker-end

2. 右键单击或打开“开发人员命令提示符”的关联菜单，再选择“固定到‘开始’菜单”或“固定到任务栏”。

## <a name="manage-files-toolbars-and-windows"></a>管理文件、工具栏和窗口

当你开发应用程序时，在任何时候都可以处理多个代码文件并且在多个工具窗口之间切换。 可以利用以下提示保持条理性：

- **使常用文件在编辑器中保持可见**。 可以将文件固定在选项卡的左侧，这样一来，无论在编辑器中打开了多少个文件，这些文件均保持可见。

   若要固定某个文件，请选择此文件的选项卡，然后选择“切换固定状态”按钮。

- **将文档和窗口移到其他监视器**。 如果您开发应用软件时使用多个监视器，则可以将编辑器中打开的文件移到另一个监视器，从而更轻松地处理应用程序的各个部分。 还可以将工具窗口（如调试器窗口）移至另一个监视器，并将文档和工具窗口以选项卡形式停靠在一起以创建“竹筏”。 有关详细信息，请参阅[在 Visual Studio 中自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)。

   还可以通过创建“解决方案资源管理器”的另一个实例并将其移至其他监视器，以便更轻松地管理文件。 若要创建“解决方案资源管理器”的另一个实例，请打开“解决方案资源管理器”中的快捷菜单，然后选择“新建解决方案资源管理器视图”。  

- **自定义在 Visual Studio 中显示的字体**。 可更改 IDE 中文本所使用的字体、字号和颜色。 例如，你可以自定义编辑器中特定代码元素的颜色以及工具窗口或整个 IDE 中的字体。 有关详细信息，请参阅[如何：更改字体和颜色](../ide/how-to-change-fonts-and-colors-in-visual-studio.md)以及[如何：更改编辑器中的字体和颜色](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)。

## <a name="see-also"></a>请参阅

- [Visual Studio 提示和技巧博客文章](https://devblogs.microsoft.com/visualstudio/visual-studio-tips-and-tricks/)
- [常用命令的默认键盘快捷键](../ide/default-keyboard-shortcuts-for-frequently-used-commands-in-visual-studio.md)
- [如何：自定义菜单和工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)
- [演练：创建简单的应用程序](../get-started/csharp/tutorial-wpf.md)
- [辅助功能提示和技巧](../ide/reference/accessibility-tips-and-tricks.md)
