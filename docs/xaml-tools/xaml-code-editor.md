---
title: XAML 代码编辑器
description: 体验 Visual Studio 中的 XAML 代码编辑器
ms.date: 06/16/2020
ms.topic: overview
monikerRange: vs-2019
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 6421fd0139b04262ac5f1e835f010c1372c034ee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85329175"
---
# <a name="xaml-code-editor"></a>XAML 代码编辑器

[Visual Studio IDE](../get-started/visual-studio-ide.md) 中的 XAML 代码编辑器包括为 Windows 平台和 [Xamarin.Forms](/xamarin/xamarin-forms/user-interface/text/editor/) 创建 WPF 和 UWP 应用时所需的所有工具。 本文概述了代码编辑器在开发基于 XAML 的应用时所扮演的角色，以及 Visual Studio 2019 中 XAML 代码编辑器特有的功能。

首先，让我们看一下包含打开的 WPF 项目的 IDE（集成开发环境）。 下图显示了将与 XAML 代码编辑器一起使用的几个关键 IDE 工具。

:::image type="content" source="media/xaml-code-editor-overview-sml.png" alt-text="Visual Studio 2019 IDE 中显示了打开的 XAML 形式的 WPF 项目" lightbox="media/xaml-code-editor-overview-lrg.png":::

从图像的左下角开始，按顺时针方向，分别是以下关键的 IDE 工具：

- [“XAML 代码编辑器”](#xaml-code-editor-ui)窗口&mdash;本文的主题&mdash;创建和编辑代码的位置。
- [XAML 设计器](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)窗口，你在该窗口中设计 UI。
- [工具箱](../ide/reference/toolbox.md)可停靠窗口，你在其中向 UI 添加控件。
- [调试](../debugger/debugger-feature-tour.md)按钮，你在其中运行代码并进行调试。 <br>（还可以在使用 [XAML 热重载](xaml-hot-reload.md)进行调试时，实时编辑代码。）
- [解决方案资源管理器](../ide/solutions-and-projects-in-visual-studio.md)窗口，可在其中管理文件、项目和解决方案。
- [属性](../ide/reference/properties-window.md)窗口，可在其中更改 UI 的外观和 UI 控件的工作方式。

若要继续，请先了解有关 XAML 代码编辑器的详细信息。

## <a name="xaml-code-editor-ui"></a>XAML 代码编辑器 UI

虽然 XAML 应用的代码编辑器窗口共享了一些 UI（用户界面）元素（这些元素也出现在标准 IDE 中），但它还提供一些独特功能，可简化 XAML 应用的开发。

下面介绍了 XAML 代码编辑器窗口本身。

![Visual Studio 中的 XAML 代码编辑器窗口](media/xaml-code-editor-window.png "Visual Studio 2019 中 XAML 代码编辑器窗口的屏幕截图")

接下来，让我们看看代码编辑器中每个 UI 元素的功能。

### <a name="first-row"></a>第一行

在 XAML 代码窗口顶部第一行左侧，有一个“设计”选项卡、“交换窗格”按钮、“XAML”选项卡和一个“弹出 XAML”按钮   。

![Visual Studio 中 XAML 代码编辑器窗口顶部两行中的第一行，其中突出显示了第一行的左侧](media/xaml-code-editor-top-row-left.png "Visual Studio 2019 中 XAML 代码编辑器窗口顶部两行中第一行的屏幕截图，其中左侧的 UI 元素突出显示")

以下是它们的工作原理：

- “设计”选项卡将焦点从 XAML 代码编辑器更改到 XAML 设计器。
- “交换窗格”按钮可反转 XAML 设计器和 XAML 代码编辑器在 IDE 中的位置。
- “XAML”选项卡将焦点更改回 XAML 代码编辑器。
- “弹出 XAML”按钮在 IDE 外部创建一个单独的 XAML 代码编辑器窗口。

在右边，依次有一个“垂直拆分”按钮，一个“水平拆分”按钮和一个“折叠窗格”按钮  。

![Visual Studio 中 XAML 代码编辑器窗口顶部两行中的第一行，其中突出显示了第一行的右侧](media/xaml-code-editor-top-row-right.png "Visual Studio 2019 中 XAML 代码编辑器窗口顶部两行中第一行的屏幕截图，其中右侧的 UI 元素突出显示")

以下是它们的工作原理：

- “垂直拆分”按钮将 XAML 设计器和 XAML 代码编辑器在 IDE 中的位置从水平对齐更改为垂直对齐。
- “水平拆分”按钮将 XAML 设计器和 XAML 代码编辑器在 IDE 中的位置从垂直对齐更改为水平对齐。
- “折叠窗格”按钮使你可以折叠底部窗格中的内容，无论是代码编辑器还是设计器。 （若要还原底部窗格，请再次选择同一按钮，该按钮现在显示为“展开窗格”。）

<!-- [!TIP]
> You can run two parallel instances of the XAML code editor concurrently by using both the **Pop Out XAML** button and the **Expand Pane** button.
>
> You might find it useful to have one larger window open that reveals more of your code in context and a smaller pane open that has its focus directly on the code that you're working on. -->

### <a name="second-row"></a>第二行

在 XAML 代码窗口顶部的第二行，有两个窗口下拉列表。 但是，如果查看这些 UI 元素的工具提示，会看到它们被进一步标识为“Element:Window”和“Member:Window”。

![Visual Studio 中 XAML 代码编辑器窗口顶部两行中的第二行，其中显示了两个窗口下拉列表](media/xaml-code-editor-top-row-windows.png "Visual Studio 2019 中 XAML 代码编辑器窗口顶部两行中第二行的屏幕截图，其中两个窗口下拉列表都可见")

窗口下拉列表具有不同的功能，如下所示：

- 左侧的“Element:Window”帮助你查看和导航到同级或父级元素。

  具体而言，它显示了一个类似于大纲的视图，展示了代码的标记结构。 从列表中选择时，代码编辑器中的焦点将与包含所选元素的代码行对齐。

    ![Visual Studio 中的Element:Window 下拉列表](media/xaml-element-window-dropdown.png "Visual Studio 2019 中Element:Window 下拉列表的屏幕截图")

- 右侧的“Member:Window”可帮助查看和导航到特性或子元素。

    具体而言，它显示了代码中的属性的列表。 从列表中选择时，代码编辑器中的焦点将与包含所选属性的代码行对齐。

    ![Visual Studio 中的Member:Window 下拉列表](media/xaml-member-window-dropdown.png "Visual Studio 2019 中Member:Window 下拉列表的屏幕截图")

### <a name="middle-pane-code-editor"></a>中间窗格，代码编辑器

中间窗格是 XAML 代码编辑器的“代码”部分。 它包含了可在 [IDE 代码编辑器](../get-started/tutorial-editor.md)中找到的大多数功能。 我们将讨论几个可以帮助开发 XAML 代码的通用 IDE 功能。 我们还会重点介绍 IDE 中特定于 XAML 的功能。

![Visual Studio 中的 XAML 代码编辑器（仅中间窗格）](media/xaml-code-editor-middle.png "Visual Studio 2019 中 XAML 代码编辑器的屏幕截图（仅中间窗格）")

#### <a name="quick-actions"></a>快速操作

可以使用[快速操作](../ide/quick-actions.md)通过单个操作重构、生成或修改代码。

例如，可以通过使用“快速操作”执行的一项有用的任务是在“MainWindow.xaml.cs”选项卡中从 C# 代码中“删除不必要的 Using” 。

以下是操作方法：

1. 将鼠标悬停在 using 语句上，选择灯泡图标，然后从下拉列表中选择“删除不必要的 Using”。

    ![IDE 编辑器“快速操作”菜单中的“删除不必要的 Using”选项](media/xaml-code-editor-remove-usings.png "IDE 编辑器“快速操作”菜单中“删除不必要的 Using”选项的屏幕截图")

1. 选择是否要修复“文档”、“项目”或“解决方案”中出现的所有匹配项  。
1. 查看“预览”对话框，然后选择“应用” 。

还可以从菜单栏中访问此功能。 为此，选择“编辑” > “IntelliSense” > “对 Using 进行删除和排序”  。

有关 Using 设置的详细信息，请参阅[对 Using 排序](../ide/reference/sort-usings.md)页面。 有关 IntelliSense 的详细信息，请参阅 [Visual Studio 中的 IntelliSense](../ide/using-intellisense.md) 页面。 此外，有关开发人员使用快速操作的一些典型方法的详细信息，请参阅[常见快速操作](../ide/common-quick-actions.md)页面。

#### <a name="change-tracking"></a>更改跟踪

左边距的颜色使你能够跟踪在文件中所做的更改。 下面是颜色与所执行操作的关系：

- 打开文件后所做的未保存的更改将由左边距上的“黄色”栏（称为选定内容的边距）表示。

    ![代码编辑器黄色栏编辑内容](media/code-editor-edit-yellow.png "代码编辑器的屏幕截图，其中在选择边距中用黄色条标记了一项更改。")

- 保存更改后（但在关闭文件前），该栏将变为“绿色”。

    ![代码编辑器绿色栏编辑内容](media/code-editor-edit-green.png "代码编辑器的屏幕截图，其中在选择边距中用绿色条标记了一项更改。")

若要禁用和启用此功能，请在“文本编辑器”设置中更改“跟踪更改”选项（“工具” > “选项” > “文本编辑器”）。

有关更改跟踪（以包括出现在代码字符串下的波浪线）的详细信息，请参阅 [Visual Studio 代码编辑器的功能](../ide/writing-code-in-the-code-and-text-editor.md)页面的“[编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md#editor-features)”&mdash;&mdash;。

#### <a name="right-click-context-menu"></a>右键单击上下文菜单

在 XAML 代码编辑器中编辑代码时，可以使用右键单击上下文菜单访问多个功能。 这些功能中的大多数在 Visual Studio IDE 中都是通用的，有些功能是在结合使用代码编辑器和设计窗口时使用的。

![Visual Studio 中的 XAML 代码编辑器的右键单击上下文菜单](media/xaml-code-editor-right-click-menu.png "Visual Studio 2019 中 XAML 代码编辑器的右键单击上下文菜单的屏幕截图")

以下是每个功能的作用以及它们的用途：

- **视图代码** - 打开“编程语言代码”窗口，该窗口通常位于包含设计窗口和 XAML 代码编辑器的默认视图旁边。
- **视图设计器** - 打开包含设计窗口和 XAML 代码编辑器的默认视图。 （如果已在默认视图中，则它不执行任何操作。）
- **快速操作和重构** - 使用单个操作重构、生成或以其他方式修改代码。 当你将鼠标悬停在代码上时，将看到一个灯泡图标，此时可以使用快速操作或重构。 <br>另请参阅：[快速操作](../ide/quick-actions.md)和[重构代码](../ide/refactoring-in-visual-studio.md)
- **重命名...** - 仅重命名命名空间。 如果没有要重命名的命名空间，则会收到一条错误消息，显示“只可以重命名命名空间前缀。”
- **对命名空间进行删除和排序** - 删除未使用的命名空间，然后对保留的命名空间进行排序。
- **速览定义** - 预览类型的定义，无需离开编辑器中的当前位置。 <br>另请参阅：[速览定义](../ide/go-to-and-peek-definition.md#peek-definition)和[使用“查看定义”查看和编辑代码](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)。
- **转到定义** - 导航到类型或成员的源，并且在新选项卡中打开结果。 <br>另请参阅：[转到定义](../ide/go-to-and-peek-definition.md#go-to-definition)。
- **环绕...** - 使用代码片段环绕，这些代码段是围绕选定的代码块添加的。 <br>另请参阅：[扩展代码片段和外侧代码片段](../ide/code-snippets.md#expansion-snippets-and-surround-with-snippets)。
- **插入代码段** - 在光标位置插入代码片段。
- **剪切** - 含义一目了然
- **复制** - 含义一目了然
- **粘贴** - 含义一目了然
- **大纲显示** - 展开和折叠部分代码。 <br>另请参阅：[大纲显示](../ide/outlining.md)。
- **源代码管理** - 查看面向开放源代码存储库的代码贡献历史记录。

### <a name="middle-pane-scroll-bar"></a>中间窗格，滚动条

滚动条的作用不仅仅在于滚动浏览代码。 还可以使用它打开另一个代码编辑器窗格。 此外，还可以借助滚动条更高效地编写代码，方法是向滚动条添加注释或使用不同的显示模式。

#### <a name="split-the-code-window"></a>拆分代码窗口

在代码编辑器的滚动条中，右上角有一个“拆分”按钮。 选择它后，可以打开另一个代码编辑器窗格。 这很有用，因为它们彼此独立操作，因此可以使用它们在不同位置处理代码。

![Visual Studio 中的 XAML 代码编辑器（仅中间窗格）](media/code-editor-split-window-button.png "Visual Studio 2019 中 XAML 代码编辑器的屏幕截图（仅中间窗格）")

有关如何拆分编辑器窗口的详细信息，请参阅[管理编辑器窗口](../ide/how-to-manage-editor-windows.md)页面。

#### <a name="use-annotations-or-map-mode"></a>使用批注或映射模式

还可以更改滚动条的呈现效果以及包含的其他功能。 例如，许多人喜欢在滚动条中包含注释，它提供诸如代码更改、断点、书签、错误和插入符号位置等视觉提示。

有些人喜欢使用映射模式，它在滚动条上以缩图形式显示代码行。 在文件中有大量代码的开发人员可能会发现映射模式能比默认滚动条更有效地跟踪代码行。

有关如何更改滚动条默认设置的详细信息，请参阅[自定义滚动条](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)页面。

## <a name="xaml-specific-features"></a>特定于 XAML 的功能

以下大多数功能在 Visual Studio IDE 中是通用的，但是其中一些功能增加了维度，使 XAML 开发人员可以更容易地编写代码。

### <a name="xaml-code-snippets"></a>XAML 代码片段

代码片段是可重用代码的小块，可以使用“右键单击”上下文菜单命令“插入代码片段”或键盘快捷方式组合（“Ctrl+K”、“Ctrl+X”）插入到代码文件中    。 我们增强了 [IntelliSense](../ide/using-intellisense.md)，使其支持显示 XAML 代码片段，这既适用于内置代码段，也适用于手动添加的任何自定义代码段。 一些现成的 XAML 片段包括 `#region`、`Column definition`、`Row definition`、`Setter` 和 `Tag`。

![XAML 代码编辑器在 IntelliSense 中显示的 XAML 代码片段选项](media/xaml-code-snippets.png "XAML 代码编辑器的屏幕截图，其中显示了 IntelliSense 中的 XAML 代码片段选项")

有关详细信息，请参阅[代码片段](../ide/code-snippets.md)和 [C# 代码片段](../ide/visual-csharp-code-snippets.md)页。

### <a name="xaml-region-support"></a>XAML #region 支持

从 Visual Studio 2015 开始，我们为 WPF 和 UWP 中的 XAML 开发人员提供了 #region 支持，最近在 [Xamarin.Forms](/xamarin/xamarin-forms/user-interface/text/editor/) 中也提供了此支持。 在 Visual Studio 2019 中，我们持续对 #region 支持进行增量改进。 例如，在[版本 16.4](/visualstudio/releases/2019/release-notes-v16.4/) 和更高版本中，会在开始键入 `<!` 时显示 #region 选项。

![XAML 代码编辑器在 IntelliSense 中显示的 #region 选项](media/code-editor-xaml-region.png "XAML 代码编辑器的屏幕截图，其中显示了 IntelliSense 中的 #region 选项")

如果要将要展开或折叠的不同部分的代码归组，可以使用区域。

```xaml
    <!--#region NameOfRegion-->
    Your code is here
    <!--#endregion-->
```

有关区域的详细信息，请参阅 [#region（C# 引用）](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region/)页面。 有关展开和折叠部分代码的详细信息，请参阅[大纲显示](../ide/outlining.md)页面。

### <a name="xaml-comments"></a>XAML 注释

开发人员通常更倾向于使用注释来记录代码。 可以通过以下方式向 MainWindow.xaml 选项卡中的 XAML 代码添加注释：

- 在注释之前输入 `<!--`，然后在注释之后添加 `-->`。
- 输入 `<!`，然后从选项列表中选择 `!--`。

  ![XAML 代码编辑器右键单击添加注释对话框](media/xaml-code-editor-comments.png "XAML 代码编辑器中用于添加注释的右键单击上下文菜单的屏幕截图")

- 选择要用注释环绕的代码，然后从 IDE 的工具栏中选择“注释”按钮。 若要反向操作，请选择“取消注释”按钮。

  ![IDE 工具栏中的“注释”按钮和“取消注释”按钮](media/comment-undo-comment-buttons.png "IDE 工具栏中的“注释”按钮和“取消注释”按钮的屏幕截图")

- 选择要用注释环绕的代码，然后按“Ctrl+K”、“Ctrl+C”   。 若要取消注释所选代码，请按“Ctrl+K”、“Ctrl+U”   。

有关如何在“MainWindow.xaml.cs”选项卡中的 C# 代码中使用注释的更多信息，请参阅[文档注释](/dotnet/csharp/language-reference/language-specification/documentation-comments/)页面。

### <a name="xaml-lightbulbs"></a>XAML 灯泡

XAML 代码中出现的灯泡图标是[快速操作](../ide/quick-actions.md)的一部分，可用于重构、生成或修改代码。

下面是几个示例，说明它们如何优化 XAML 编码体验：

- **删除不必要的命名空间。** 在 XAML 代码编辑器中，不必要的命名空间以灰色文本显示。 如果将光标悬停在不必要的 using 上，会出现一个灯泡。 如果从下拉列表中选择“删除不必要的命名空间”选项，会显示可以删除的命名空间的预览。

  ![XAML 代码编辑器在“快速操作”灯泡中显示的“删除不必要的命名空间”选项](media/xaml-code-editor-dimmed-namespaces-preview.png "XAML 代码编辑器的“删除不必要的命名空间”选项的屏幕截图，该选项使用“快速操作”灯泡显示")

- **重命名命名空间**。 该功能可以在突出显示命名空间后，从右键单击上下文菜单中获得，这样可便于同时更改多个设置实例。 还可以使用菜单栏（“编辑” > “重构” > “重命名”），或者按“Ctrl+R”，然后再次按“Ctrl+R”，来访问此功能      。

  ![XAML 代码编辑器的右键单击上下文菜单中的“重命名命名空间”选项](media/code-editor-rename-namespace.png "XAML 代码编辑器的“重命名命名空间”选项的屏幕截图，该选项使用右键单击上下文菜单显示")

  有关详细信息，请参阅[“重命名代码符号”重构](../ide/reference/rename.md)页。

### <a name="conditional-xaml-for-uwp"></a>UWP 的条件 XAML

条件 XAML 提供在 XAML 标记中使用 ApiInformation.IsApiContractPresent 方法的一种途径。 可以在 API 存在的情况下在标记中设置属性和实例化对象，无需使用代码隐藏。

有关详细信息，请参阅[条件 XAML](/windows/uwp/debug-test-perf/conditional-xaml/) 页面和[桌面应用中的主机 UWP XAML 控件（XAML Islands）](/windows/apps/desktop/modernize/xaml-islands/)页面。

### <a name="xaml-structure-visualizer"></a>XAML 结构可视化工具

代码编辑器中的结构可视化工具功能可显示结构参考线，这些参考线是垂直虚线，指明代码中匹配的打开和关闭标记元素。 这些垂直线使你可以更加轻松地判断逻辑块的开始和结束位置。

有关详细信息，请参阅[导航代码](../ide/navigating-code.md)页面。

### <a name="intellicode-for-xaml"></a>适用于 XAML 的 IntelliCode

将 XAML 标记添加到代码中时，通常以左尖括号 `<` 开头。 键入尖括号时，将出现一个 IntelliCode 菜单，其中列出了几个比较常见的 XAML 标记。 选择可用于将其快速添加到代码中的选项。

可以识别所选的 IntelliCode 内容，因为它们显示在列表的顶部，并带有星号。

![XAML 文本编辑器的 IntelliCode 列表](media/xaml-intellicode-selection.png "XAML 文本编辑器的 IntelliCode 列表的屏幕截图")

有关详细信息，请参阅 [IntelliCode 概述](/visualstudio/intellicode/overview/)页。

### <a name="settings"></a>设置

有关 Visual Studio IDE 中所有设置的详细信息，请参阅[代码编辑器的功能](../ide/writing-code-in-the-code-and-text-editor.md)页面。

## <a name="xaml-optional-settings"></a>XAML 可选设置

可以使用[选项](../ide/reference/options-dialog-box-visual-studio.md)对话框更改 XAML 代码编辑器的默认设置。 若要查看设置，请选择“工具” > “选项” > “文本编辑器” > “XAML”   。

![XAML 文本编辑器的“选项”列表](media/xaml-tools-options.png "XAML 文本编辑器的选项列表的屏幕截图")

> [!NOTE]
> 也可以使用键盘快捷方式访问“选项”对话框。 操作方法如下：按“Ctrl+Q”搜索 IDE，键入“选项”，然后按“Enter”   。 接下来，按“Ctrl+E”搜索“选项”对话框，键入“文本编辑器”，按“Enter”，键入“XAML”，然后按“Enter”     。
>  
> 有关键盘快捷方式的详细信息，请参阅 [Visual Studio 的快捷方式提示](../ide/productivity-shortcuts.md#code-editor)页。

### <a name="universal-text-editor-options"></a>通用文本编辑器选项

在 XAML 的“[选项](../ide/reference/options-text-editor-xaml-formatting.md)”对话框中，以下前三项对于 Visual Studio IDE 支持的所有编程语言都是通用的。 可访问下表中的链接信息，了解有关这些选项以及如何使用它们的详细信息。

|名称  |更多信息  |
|---------|---------|
|常规  | [“选项”对话框：“文本编辑器”>“所有语言”](../ide/reference/options-text-editor-all-languages.md) |
|滚动栏 | [“选项”-&gt;“文本编辑器”-&gt;“所有语言”-&gt;“滚动条”](../ide/reference/options-text-editor-all-languages-scroll-bars.md) |
|制表符  |  [“选项”->“文本编辑器”->“所有语言”->“选项卡”](../ide/reference/options-text-editor-all-languages-tabs.md) |

### <a name="xaml-specific-text-editor-options"></a>特定于 XAML 的文本编辑器选项

下表列出了[选项](../ide/reference/options-text-editor-xaml-formatting.md)对话框中的设置，这些设置可以优化开发基于 XAML 的应用时的编辑体验。 请访问链接信息，了解有关这些选项以及如何使用它们的详细信息。

|名称  |更多信息  |
|---------|---------|
|格式设置 | [选项，文本编辑器，XAML，格式](../ide/reference/options-text-editor-xaml-formatting.md) |
|其他 |  [选项, 文本编辑器, XAML, 杂项](../ide/reference/options-text-editor-xaml-miscellaneous.md) |

> [!TIP]
> “杂项”部分中的“事件处理程序方法名称首字母大写”设置对 XAML 开发人员特别有用 。 因为是新设置，所以在默认情况下是“关闭”状态，但建议将其设置为“开启”，以获取代码中的正确大小写支持 。

## <a name="next-steps"></a>后续步骤

若要了解在调试模式下运行应用时如何实时编辑代码的详细信息，请参阅 [XAML 热重载](xaml-hot-reload.md)页面。

## <a name="see-also"></a>请参阅

- [Visual Studio 代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview/)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)
- [Xamarin 移动应用开发 (Mac)](/visualstudio/mac/xamarin/)
- [Visual Studio 2019 for Mac - IDE 导览 (Mac)](/visualstudio/mac/ide-tour/)
