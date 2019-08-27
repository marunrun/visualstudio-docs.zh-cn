---
title: 在代码和文本编辑器中编写代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.texteditor
dev_langs:
- JScript
- VB
- CSharp
helpviewer_keywords:
- code editor, word wrap
- outlining
- code, editing
- squiggles
- code editor, outlining
- code editor, error and warning markers
- word wrap
- code editor, syntax coloring
- code editor, go to definition
- diff
- code editor [Visual Studio]
- code editor, diff
- error and warning markers
- code editor, navigation bar
- code editor, customizing
- comment selection
- code editor, tabify
- brace matching
- code editor, line numbers
- printing
- code editor, brace matching
- code editor, squiggles
- code editor, features
- line numbers
- go to definition
- syntax coloring
- code editor, navigate to
- code editor, comparing files
- code editor, zoom
- code editor
- code files
- go to line
- tabify
- zoom
- navigate to
- line break characters
- code editor, virtual space
- code editor, change tracking
- code editor, comment selection
- code editor, printing
- virtual space
- code editor, line break characters
- code editor, go to line
- code
ms.assetid: cb53ab9a-5b76-4759-b9e8-7bf32298ecbe
caps.latest.revision: 46
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 23dd08e95100f186c172fff2cfa6a392bd11eee4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698091"
---
# <a name="writing-code-in-the-code-and-text-editor"></a>在代码和文本编辑器中编写代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Visual Studio 编辑器提供了许多功能，让你可以更轻松地编写和管理自己的代码。 可通过使用大纲显示来展开和折叠不同的代码块。 可通过使用 IntelliSense、“对象浏览器”  以及调用层次结构，了解有关正在使用的代码的详细信息。 可通过使用“定位到”  、“转到定义”  和“查找所有引用”  等功能在代码内部导航。 可以将插入代码块和代码片段，并且可以通过“使用时生成”  等功能生成代码。 如果之前从未使用过 Visual Studio 2015 编辑器，则请参阅 [编辑代码](https://www.visualstudio.com/features/ide-vs) 进行快速了解。  

 可以使用多种不同的方式查看自己的代码。 若要查看解决方案的类视图，可以打开“类视图”  窗口或展开类文件下“解决方案资源管理器”  中的节点。  

 可以搜索和替换单个或多个文件的文本。 有关详细信息，请参阅[查找和替换文本](../ide/finding-and-replacing-text.md)。 如果使用正则表达式，则请注意：查找和替换现在使用 .NET 正则表达式。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。  

 不同的 Visual Studio 语言提供不同的功能集，在某些情况下，同样的功能在不同语言中的行为也会有所不同。 功能说明中已指出多数差异，但如需有关详细信息，可以参阅特定 Visual Studio 语言相关章节。  

> [!IMPORTANT]
> 正在使用的 Visual Studio 版本和设置可能会影响 IDE 中的功能。 它们可能与本主题中介绍的功能有所不同。  

## <a name="editor-features"></a>编辑器功能  

|||  
|-|-|  
|语法着色|用不同颜色对代码和标记文件中某些语法元素着色，从而将它们区分开来。 例如，关键字（如 C# 中的 `using` 和 Visual Basic 中的 `Imports` ）用一种颜色，类型（如 `Console` 和 `Uri`用另一种颜色。 也为其他语法元素（如字符串文本和注释）着色。 C++ 使用颜色来区分类型、枚举、宏以及其他标记。<br /><br /> 可以看到每种类型的默认颜色，并且可以更改可从“工具”菜单打开的 [Fonts and Colors, Environment, Options Dialog Box](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)中任意特定语法元素的颜色  。|  
|错误和警告标记|添加代码和生成解决方案时，可能会看到 (a) 不同颜色的波浪下划线（称为波形曲线）或者 (b) 灯泡显示在你的代码中。 红色波浪线表示语法错误，蓝色表示编译器错误，绿色表示警告，而紫色表示其他类型的错误。 [灯泡](../ide/perform-quick-actions-with-light-bulbs.md) 建议了问题的修补程序，并简化修补程序的应用。<br /><br /> 可在“工具/选项/环境/字体和颜色”  对话框中看到每种错误和警告曲线的默认颜色。 查找“语法错误”  、“编译器错误”  、“警告”  和“其他错误”  。|  
|括号匹配|插入点放置在代码文件中的左大括号上时，将突出显示左大括号和右大括号。 此功能可为你提供有关错放或丢失大括号的即时反馈。 可以使用“自动突出显示分隔符”  设置来启用或禁用大括号匹配（“工具/选项/文本编辑器”  ）。 可以在“字体和颜色”  设置中更改突出显示颜色（“工具/选项/环境”  ）。 查找“大括号匹配（突出显示）”  或“大括号匹配（方括号）”  。|  
|行号|可在代码窗口的左边距中显示行号。 默认情况下不显示行号。 可在“文本编辑器的所有语言”  设置中启用此选项（“工具/选项/文本编辑器/所有语言”  ）。 可以通过更改各编程语言的设置来显示其行号（“工具/选项/文本编辑器/\<语言>”  ）。 对于要打印的行号，则必须在“打印”  对话框中选择“包括行号”。|  
|更改跟踪|左边距的颜色使你能够跟踪在文件中所做的更改。 打开文件后所做的未保存的更改将由左边距上的黄色栏（称为选定内容的边距）表示。 保存更改后（但在关闭文件前），该栏将变为绿色。 如果在保存文件后撤消更改，则该栏将变为橙色。 若要禁用和启用此功能，请在“文本编辑器”  设置中更改“跟踪更改”  选项（“工具/选项/文本编辑器”  ）。|  
|选择代码和文本|可以在标准的连续流模式或框模式中选择文本，你将在其中选择一个矩形部分的文本而非一组文本行。 若要在框模式中进行选择，请在将鼠标拖到选定内容上时按下 Alt 键（或按 Alt + Shift + \<箭头键>）。 选定内容包括由所选范围中第一个字符和最后一个字符所定义的矩形内的所有字符。 键入或粘贴到所选区域内的任何内容均将在每行中的相同点插入。|  
|缩放|可以通过按住 CTRL 键并移动鼠标滚轮（或按 CTRL + SHIFT + . 进行放大，CTRL + SHIFT + , 进行缩小）在任何代码窗口中进行放大或缩小。 可以使用代码窗口左下角的“缩放”框设置特定的缩放百分比。 缩放功能不适用于工具窗口。|  
|虚空格|默认情况下，Visual Studio 编辑器中的行在最后一个字符后结束，从而行尾的向右键会将光标移到下一行的开头。 在某些其他编辑器中，行并不在最后一个字符后结束，你可以将光标放置在行上的任意位置。 可以在“工具/选项/文本编辑器/所有语言”  设置中启用编辑器中的虚空格。 请注意，可以启用“虚空格”  或“自动换行”  之一，但不能同时启用这两者。|  
|打印|打印文件时，可以使用“打印”  对话框中的选项来包括行号或隐藏折叠的代码区域。 在“页面设置”  对话框中，还可以通过选择“页面页眉”  来打印完整路径及文件名。<br /><br /> 可以在“工具/选项/环境/字体和颜色”  对话框中设置颜色打印选项。 在“显示以下对象的设置”  列表中选择“打印机”  ，以自定义彩色打印。 可以为打印文件而非编辑文件指定不同的颜色。|  
|全局撤消和重做|“编辑”  菜单上的“撤消上次全局操作”  和“重做上一全局操作”  命令可撤消或重做影响多个文件的全局操作。 全局操作包括重命名类或命名空间、在解决方案中执行查找和替换操作、重构数据库或更改多个文件的任何其他操作。 可对当前 Visual Studio 会话中的操作应用全局撤消和重做命令（甚至在关闭应用操作的解决方案之后）。|  

## <a name="advanced-editing-features"></a>高级编辑功能  
 可以在“编辑/高级”  子菜单中找到许多高级功能。 并非所有这些功能都可用于所有类型的代码文件。  

|||  
|-|-|  
|设置文档的格式|设置适当的代码行缩进，并移动大括号以分隔文档中的行。|  
|设置选定内容的格式|设置适当的代码行缩进，并移动大括号以分隔选定内容中的行。|  
|将选定行中的空格替换为制表符|在适当的位置将前导空格更改为选项卡。|  
|将选定行中的制表符替换为空格|将前导制表符更改为空格。 如果要将文件中的所有空格都转换为制表符（或将所有制表符转换为空格），可以使用 `Edit.ConvertSpacesToTabs` 和 `Edit.ConvertTabsToSpaces` 命令。 这些命令不会出现在 Visual Studio 菜单中，但可以从快速访问窗口或命令窗口中进行调用。|  
|转换为大写|将选定内容中的所有字符更改为大写；如果未选择任何内容，则将插入点处的字符更改为大写。|  
|转换为小写|将选定内容中的所有字符更改为小写；如果未选择任何内容，则将插入点处的字符更改为小写。|  
|验证文档|验证 JScript 代码文件。|  
|删除水平空白|删除当前行末尾的制表符或空格。|  
|查看空白|将空格显示为上移的点，将制表符显示为箭头。 文件末尾将显示为矩形标志符号。 如果已选择“工具/选项/文本编辑器/所有语言/自动换行/显示可见的自动换行标志符号”  ，则也将显示该标志符号。|  
|自动换行|使文档中的所有行在代码窗口中均可见。 可以在“文本编辑器的所有语言”设置中禁用和启用自动换行（“工具/选项/文本编辑器/所有语言”  ）。|  
|取消注释选定内容|向选定内容或当前行添加注释字符。|  
|注释选定内容|从选定内容或当前行删除注释字符。|  
|增加行缩进|向所选行或当前行添加一个制表符（或等效空格）。|  
|减少行缩进|从所选行或当前行删除一个制表符（或等效空格）。|  
|选择标记|在包含标记（如 XML 或 HTML）的文档中选择标记。|  
|选择标记内容|在包含标记（如 XML 或 HTML）的文档中选择内容。|  

## <a name="navigate-in-the-code-window"></a>在代码窗口中导航  
 可以使用多种不同的方式在文档中移动。 除标准操作外，还可以使用工具栏上的“向后导航”  （或 CTRL + 减号）和“向前导航”  （CTRL + SHIFT + 减号）按钮将插入点移动到先前位置，或返回活动文档中更新的位置。 这些按钮保留插入点的最后 20 个位置。  

 ![向前和向后导航按钮](../ide/media/vs2015-nav-buttons.png "VS2015_Nav_buttons")  

 也可以在代码窗口中使用增强的滚动条来获取代码的鸟瞰视图。 映射模式下，可向上移动光标和向下滚动条，有关详细信息，请参阅代码的预览，请参阅[如何：通过自定义滚动条来跟踪代码](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)。  

 以下命令是特定于代码的导航方法：  

|||  
|-|-|  
|转到 \<行号>|(**编辑/转到**或 CTRL + G):移动到活动文档中的特定行号。|  
|定位到|(**编辑/导航到**或 CTRL +，):活动解决方案中查找符号或文件。 它帮助你从查询中选取一组很好的匹配结果。 可通过使用 Camel 大小写格式和下划线字符将符号分为关键字，从而搜索符号中包含的关键字。|  
|查找所有引用|（上下文菜单）：在解决方案中查找对选定元素的所有引用。|  
|转到定义|（上下文菜单或 F12）：查找所选元素的定义。|  
|查看定义|（上下文菜单或 Alt + F12）：查找所选元素的定义，并将其显示在弹出窗口。 有关详细信息，请参阅[如何：查看和编辑代码使用查看定义 (Alt + F12)](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)。|  
|下一个方法，上一个方法|（“编辑/下一个方法，上一个方法”  ）在 Visual Basic 代码文件中，使用这些命令将插入点移动到不同的方法。|  
|引用突出显示|单击源代码中的符号时，将在文档中突出显示该符号的所有实例。 突出显示的符号可能包括声明和引用，以及许多其他“查找所有引用”  将返回的符号。 其中包括类、对象、变量、方法和属性的名称。 在 Visual Basic 代码中，也将突出显示许多控件结构的关键字。 若要移至下一个或上一个突出显示的符号，请按 CTRL+SHIFT+向下键或 CTRL+SHIFT+向上键。 可以在“工具/选项/环境/字体和颜色/突出显示的引用” |  
|查找代码相关信息|在代码编辑器中使用 CodeLens 时，可以找到有关特定代码的信息，如更改和更改者、引用、Bug、工作项、代码评审和单元测试状态。 将 Visual Studio Enterprise 与 Team Foundation Server 一起使用时，CodeLens 的工作原理类似于警告显示。 请参阅[查找代码更改和其他历史记录](../ide/find-code-changes-and-other-history-with-codelens.md)。|  

 还可以使用“导航栏”  （即显示在代码窗口顶部的两个下拉框）在代码文件中导航。 此栏使你能够直接定位到特定类型或类型中的成员之一。 导航栏将与 Visual Basic、C# 和 C++ 代码文件一起显示。  

 若要隐藏导航栏，请更改“文本编辑器的所有语言”设置中的“导航栏”  选项（“工具/选项/文本编辑器/所有语言”  ，或者可以更改各语言的设置）。 可在下拉框中导航，如下所示：  

- 若要将焦点从代码窗口切换到导航栏，请按快捷组合键 CTRL+F2。  

- 若要将焦点从导航栏返回到代码窗口，请按 ESC 键。  

- 若要在导航栏上的项之间切换焦点，请按 TAB 键。  

- 若要选择具有焦点的导航栏项并返回 IDE，请按 ENTER 键  

- 若要定位到类或类型，请在左侧的下拉列表中单击其名称。  

- 若要直接定位到类中的过程，请单击右侧下拉列表中的过程。  

  分部类中，在当前代码文件外部定义的成员可能会显示为灰色。  

## <a name="find-code-using-navigate-to"></a>使用“导航到”查找代码
Visual Studio 的“导航到”命令会对代码进行重点搜索，帮助用户在代码文件、文件路径和代码符号中快速找到指定的元素。 与其他文本搜索（例如“查找”或“在文件中查找”）不同的是，“导航到”会将其搜索范围限制为实际代码所在的区域，例如文件、窗体和代码模块。 例如，在 ASP.NET Web 应用程序中搜索某个字符串时，如果在整个解决方案中使用“查找”或“在文件中查找”，则有可能收到多个匹配项，包括代码注解中字符串的实例。 通过使用导航到，但是，你可能只能获取单个函数，而忽略代码注解中字符串的任何实例。

### <a name="navigate-code-using-navigate-to"></a>使用“导航到”导航代码

1. 在 Visual Studio 中打开解决方案或文件夹。
1. 在主菜单中，选择“编辑”  、“导航到”  ，或按“Ctrl + ,”  。

    代码编辑器的上方会出现一个小文本框。
1. 在文本框中，输入要查找的代码元素的名称。

    ![“导航到”窗口](../ide/media/vside-navigatetowindow.png "“导航到”窗口")

    键入内容时，结果显示在文本框下的下拉列表中。
1. 若要转到某个元素，请在列表中选择它。

### <a name="filter-your-search"></a>筛选搜索

若要限制搜索范围以仅代码符号，前面加上与在导航到查询"\@"字符。 例如，如果搜索 `@application`，“导航到”只会显示其中包含单词“application”的类。

如果在代码中使用骆驼拼写法，则可以通过仅输入代码元素名称的大写字母，更快地找到代码元素。 例如，如果代码有一个名为 `ViewSwitcher` 的组件，则可以通过在“导航到”窗口中仅输入该名称的大写字母 (`"VS"`) 来找到它。

![“导航到”窗口 - 使用大写字母搜索](../ide/media/vside-capitalsearch.png "“导航到”窗口 - 使用大写字母搜索")

此功能在代码名称很长的情况下特别有用。

## <a name="customize-the-editor"></a>自定义编辑器  
 **导入和导出设置**:可以与其他开发人员共享设置，使自己的设置符合标准，或者通过使用 Visual Studio 的默认设置为返回**导入和导出设置向导**上**工具**菜单。 可以更改常规设置或特定于语言和项目的设置。  

 **键盘映射**:可以定义新热键或重新定义现有热键的工具/选项/环境/键盘设置中。 有关热键的详细信息，请参阅[默认键盘快捷键](../ide/default-keyboard-shortcuts-in-visual-studio.md)。  

 有关特定于语言的编辑器选项的信息，请参阅以下内容：  

- [Visual Basic 设置](https://msdn.microsoft.com/library/2712b3b1-18f2-430c-ae91-28468bbf5f32)  

- [使用 Visual Studio C# 开发环境](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)  

- [“选项”->“文本编辑器”->“JavaScript”->“格式设置”](../ide/reference/options-text-editor-javascript-formatting.md)  

## <a name="in-this-section"></a>本节内容  

- [查找和替换文本](../ide/finding-and-replacing-text.md)  

- [编码和换行符](../ide/encodings-and-line-breaks.md)  

- [大纲显示](../ide/outlining.md)  

- [重构](../ide/refactoring-in-visual-studio.md)  

- [工作效率提示](../ide/productivity-tips-for-visual-studio.md)  

- [使用 IntelliSense](../ide/using-intellisense.md)  

- [自定义编辑器](../ide/customizing-the-editor.md)  

- [如何：通过自定义滚动条来跟踪代码](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)  

- [如何：使用“查看定义”(Alt+F12) 查看和编辑代码](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)  

- [使用灯泡执行快速操作](../ide/perform-quick-actions-with-light-bulbs.md)  

- [代码片段](../ide/code-snippets.md)  

- [使用工具箱](../ide/using-the-toolbox.md)  

- [查看代码的结构](../ide/viewing-the-structure-of-code.md)  

- [在代码中设置书签](../ide/setting-bookmarks-in-code.md)  

- [使用任务列表](../ide/using-the-task-list.md)  

- [查找代码更改和其他历史记录](../ide/find-code-changes-and-other-history-with-codelens.md)  

## <a name="see-also"></a>请参阅  
 [Visual Studio IDE](../ide/visual-studio-ide.md)
