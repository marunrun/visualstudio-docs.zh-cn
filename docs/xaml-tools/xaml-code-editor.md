---
title: XAML 代码编辑器
ms.date: 06/16/2020
ms.topic: conceptual
monikerRange: vs-2019
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: d789ac099e6d0bba7a44f0d6efd7a19beec54c19
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289655"
---
# <a name="xaml-code-editor"></a>XAML 代码编辑器

[Visual STUDIO IDE](../get-started/visual-studio-ide.md)中的 XAML 代码编辑器包含为 Windows 平台和[Xamarin](/xamarin/xamarin-forms/user-interface/text/editor/)创建 WPF 和 UWP 应用所需的所有工具。 本文概述了在开发基于 XAML 的应用时代码编辑器所扮演的角色，以及 Visual Studio 2019 中的 XAML 代码编辑器特有的功能。

首先，让我们看一下 IDE （集成开发环境），其中包含一个打开的 WPF 项目。 下图显示了将与 XAML 代码编辑器一起使用的几个关键 IDE 工具。

:::image type="content" source="media/xaml-code-editor-overview-sml.png" alt-text="Visual Studio 2019 IDE （包含 XAML 中的打开的 WPF 项目）" lightbox="media/xaml-code-editor-overview-lrg.png":::

从图像的左下角沿顺时针方向，主要的 IDE 工具如下：

- 在**[XAML 代码编辑器](#xaml-code-editor-ui)** 窗口 &mdash; &mdash; 中，您可以在其中创建和编辑您的代码。
- **[XAML 设计器](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)** 窗口，您可以在其中设计用户界面。
- **[工具箱](../ide/reference/toolbox.md)** 可停靠窗口，可在其中将控件添加到 UI。
- **[调试](../debugger/debugger-feature-tour.md)** 按钮，你可以在其中运行代码并对其进行调试。 <br>（你还可以在通过[XAML 热重载](xaml-hot-reload.md)进行调试的同时实时编辑代码。）
- "**[解决方案资源管理器](../ide/solutions-and-projects-in-visual-studio.md)**" 窗口，您可以在该窗口中管理文件、项目和解决方案。
- "**[属性](../ide/reference/properties-window.md)**" 窗口，您可以在其中更改 ui 的外观和 ui 控件的工作方式。

若要继续，请了解有关 XAML 代码编辑器的详细信息。

## <a name="xaml-code-editor-ui"></a>XAML 代码编辑器 UI

虽然 XAML 应用程序的 "代码编辑器" 窗口共享了一些也出现在标准 IDE 中的 UI （用户界面）元素，但它还包括一些使开发 XAML 应用更容易的独特功能。

下面介绍了 XAML 代码编辑器窗口本身。

![Visual Studio 中的 XAML 代码编辑器窗口](media/xaml-code-editor-window.png "Visual Studio 2019 中 "XAML 代码编辑器" 窗口的屏幕截图")

接下来，让我们看看代码编辑器中每个 UI 元素的功能。

### <a name="first-row"></a>第一行

在 "XAML 代码" 窗口顶部的第一行中，有一个 "**设计**" 选项卡、"**交换窗格**" 按钮、" **XAML** " 选项卡和 "**弹出 xaml** " 按钮。

![Visual Studio 中 "XAML 代码编辑器" 窗口的第一个前两行，其中突出显示了第一行的左侧](media/xaml-code-editor-top-row-left.png "Visual Studio 2019 中 "XAML 代码编辑器" 窗口的第一行的第一列的屏幕截图，左侧的 UI 元素将突出显示")

下面是它们的工作原理：

- "**设计**" 选项卡将焦点从 XAML 代码编辑器更改为 XAML 设计器。
- "**交换窗格**" 按钮在 IDE 中反转 XAML 设计器的位置和 XAML 代码编辑器。
- " **Xaml** " 选项卡会将焦点更改回 XAML 代码编辑器。
- "**弹出 xaml** " 按钮创建一个位于 IDE 之外的单独的 XAML 代码编辑器窗口。

在右侧，有一个**垂直拆分**按钮、一个**水平拆分**按钮和一个**折叠窗格**按钮。

![Visual Studio 中 "XAML 代码编辑器" 窗口的第一个前两行，其中突出显示了第一行的右侧](media/xaml-code-editor-top-row-right.png "Visual Studio 2019 中 "XAML 代码编辑器" 窗口的第一行的第一列的屏幕截图，其中突出显示了右侧的 UI 元素")

下面是它们的工作原理：

- **垂直拆分**按钮将 IDE 中的 XAML 设计器位置和 XAML 代码编辑器从水平对齐方式更改为垂直对齐。
- **水平拆分**按钮将 IDE 中的 XAML 设计器位置和 XAML 代码编辑器从垂直对齐方式更改为水平对齐方式。
- **折叠窗格**按钮可用于折叠底部窗格中的内容，无论它是代码编辑器还是设计器。 （若要还原底部窗格，请再次选择同一按钮，该按钮现在命名为**展开窗格**按钮。）

<!-- [!TIP]
> You can run two parallel instances of the XAML code editor concurrently by using both the **Pop Out XAML** button and the **Expand Pane** button.
>
> You might find it useful to have one larger window open that reveals more of your code in context and a smaller pane open that has its focus directly on the code that you're working on. -->

### <a name="second-row"></a>第二行

在 "XAML 代码" 窗口顶部的第二行中，有两个窗口下拉列表。 但是，如果您查看这些 UI 元素的工具提示，它会进一步将它们标识为 "Element： Window" 和 "Member： Window"。

![Visual Studio 中 "XAML 代码编辑器" 窗口的第二行中的第二行，其中两个窗口下拉列表都可见](media/xaml-code-editor-top-row-windows.png "Visual Studio 2019 中 "XAML 代码编辑器" 窗口的第二行的第二行屏幕截图，其中两个窗口下拉列表都可见")

窗口下拉列表具有不同的功能，如下所示：

- 左侧的 "**元素：" 窗口**可帮助你查看和导航到同级或父元素。

  具体而言，它会显示一个类似大纲的视图，该视图可显示代码的标记结构。 从列表中选择时，"代码编辑器" 中的焦点将与包含所选元素的代码行对齐。

    ![Visual Studio 中的 "元素：窗口" 下拉列表](media/xaml-element-window-dropdown.png "Visual Studio 2019 中 "元素：窗口" 下拉列表的屏幕截图")

- 右侧的 "**成员：" 窗口**可帮助你查看和导航到特性或子元素。

    具体而言，它显示代码中的属性列表。 从列表中选择时，"代码编辑器" 中的焦点将与包含所选属性的代码行对齐。

    ![Visual Studio 中的 "成员：窗口" 下拉列表](media/xaml-member-window-dropdown.png "Visual Studio 2019 中 "成员：窗口" 下拉列表的屏幕截图")

### <a name="middle-pane-code-editor"></a>中间窗格，代码编辑器

中间窗格是 XAML 代码编辑器的 "代码" 部分。 它包含您将在[IDE 代码编辑器](../get-started/tutorial-editor.md)中找到的大多数功能。 我们将介绍一些可帮助你开发 XAML 代码的通用 IDE 功能。 此外，我们还将突出显示 IDE 中的唯一到 XAML 功能。

![Visual Studio 中的 XAML 代码编辑器（仅限中间窗格）](media/xaml-code-editor-middle.png "Visual Studio 2019 中的 XAML 代码编辑器的屏幕截图（仅限中间窗格）")

#### <a name="quick-actions"></a>快速操作

您可以使用 "[快速操作](../ide/quick-actions.md)"，通过单个操作来重构、生成或修改代码。

例如，使用 "快速操作" 可以执行的一项有用的任务是从**MainWindow.xaml.cs**选项卡中的 c # 代码中**删除不必要的 using** 。

操作方法如下：

1. 将鼠标悬停在 using 语句上，选择灯泡图标，然后从下拉列表中选择 "**删除不必要的 using** "。

    !["快速操作" 菜单中的 "删除不必要的 Using" 选项](media/xaml-code-editor-remove-usings.png ""快速操作" 菜单中的 IDE 编辑器删除不必要的 Using 选项的屏幕截图")

1. 选择是否要修复**文档**、**项目**或**解决方案**中的所有匹配项。
1. 查看**预览**对话框，然后选择 "**应用**"。

您还可以从菜单栏中访问此功能。 为此，请选择 "**编辑**  >  **IntelliSense**" "  >  **删除并排序**"。

有关 using 设置的详细信息，请参阅[Sort using](../ide/reference/sort-usings.md)页。 有关 IntelliSense 的详细信息，请参阅[Visual Studio 中的 intellisense](../ide/using-intellisense.md)页面。 而且，有关开发人员使用快速操作的一些典型方法的详细信息，请参阅常见的 "[快速操作](../ide/common-quick-actions.md)" 页。

#### <a name="change-tracking"></a>Change tracking

左边距的颜色使你能够跟踪在文件中所做的更改。 下面是颜色与所执行操作的关系：

- 自文件打开后所做的更改，但未保存的更改将由左边距上的**黄色**条表示（称为选择边距）。

    !["代码编辑器" 编辑黄色栏](media/code-editor-edit-yellow.png "代码编辑器的屏幕截图，其中的更改在选择边距中标记为黄色条。")

- 保存更改后（但在关闭文件前），此栏将变为**绿色**。

    !["代码编辑器" 编辑为绿色栏](media/code-editor-edit-green.png "代码编辑器的屏幕截图，其中的更改在选择边距中标记为绿色条。")

若要关闭和打开此功能，请在 "**文本编辑器**" 设置中更改 "**跟踪更改**" 选项（"**工具**" "选项" "  >  **Options**  >  **文本编辑器**"）。

有关更改跟踪 &mdash; 以包括显示在 "代码字符串" 下的波浪线（也称为 "波形曲线"）的详细信息， &mdash; 请参阅[Visual Studio Code 编辑器的功能](../ide/writing-code-in-the-code-and-text-editor.md)的**[编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md#editor-features)** 部分。

#### <a name="right-click-context-menu"></a>右键单击上下文菜单

当你在 XAML 代码编辑器中编辑代码时，可以使用右键单击上下文菜单来访问一些功能。 大多数这些功能在 Visual Studio IDE 中都是通用的，而有些功能则特定于使用代码编辑器和设计窗口。

![Visual Studio 中的 XAML 代码编辑器的右键单击上下文菜单](media/xaml-code-editor-right-click-menu.png "Visual Studio 2019 中的 XAML 代码编辑器右键单击上下文菜单的屏幕截图")

下面介绍了每个功能的作用，并说明了其用途：

- "**查看代码**"-打开 "编程语言代码" 窗口，该窗口通常选项卡在包括 "设计" 窗口和 XAML 代码编辑器的默认视图旁边。
- **视图设计器**-打开包含设计窗口和 XAML 代码编辑器的默认视图。 （如果已在默认视图中，则不执行任何操作。）
- **快速操作和重构**-重构，生成，或以其他方式使用单个操作修改代码。 当你将鼠标悬停在代码上时，你会在快速操作或重构可用时看到一个灯泡图标。 <br>另请参阅：[快速操作](../ide/quick-actions.md)和[重构代码](../ide/refactoring-in-visual-studio.md)。
- **重命名 ...**-仅重命名命名空间。 如果没有要重命名的命名空间，则将收到一条错误消息，显示 "只能重命名命名空间前缀"。
- **删除命名空间并对其进行排序**-删除未使用的命名空间，然后对这些命名空间进行排序。
- **速览 definition** -预览类型的定义，而无需离开编辑器中的当前位置。 <br>另请参阅：[速览定义](../ide/go-to-and-peek-definition.md#peek-definition)并[使用查看定义查看和编辑代码](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)。
- **转到定义**-导航到类型或成员的源，并在新选项卡中打开结果。 <br>另请参阅：[中转到 "定义](../ide/go-to-and-peek-definition.md#go-to-definition)"。
- **外侧代码 ...**-使用围绕所选代码块添加的外侧代码片段。 <br>另请参见：[扩展代码段和外侧代码段](../ide/code-snippets.md#expansion-snippets-and-surround-with-snippets)。
- **插入代码片段**-在光标位置插入代码片段。
- **剪切**-一目了然
- **复制**-一目了然
- **粘贴**-一目了然
- **大纲显示**代码的展开和折叠部分。 <br>请参见：[大纲显示](../ide/outlining.md)。
- **源代码管理**-查看开源存储库中的代码贡献历史记录。

### <a name="middle-pane-scroll-bar"></a>中间窗格，滚动条

滚动条除了滚动浏览代码外，可以执行更多操作。 你还可以使用它打开其他代码编辑器窗格。 而且，您可以使用滚动条通过向其添加批注或使用不同的显示模式来帮助您更有效地编码。

#### <a name="split-the-code-window"></a>拆分代码窗口

在代码编辑器的滚动条中，在右上角有一个**拆分**按钮。 选择它时，可以打开另一个代码编辑器窗格。 这非常有用，因为它们彼此独立地运行，因此，你可以使用它们来处理不同位置中的代码。

![Visual Studio 中的 XAML 代码编辑器（仅限中间窗格）](media/code-editor-split-window-button.png "Visual Studio 2019 中的 XAML 代码编辑器的屏幕截图（仅限中间窗格）")

有关如何拆分编辑器窗口的详细信息，请参阅 "[管理编辑器](../ide/how-to-manage-editor-windows.md)" 窗口页。

#### <a name="use-annotations-or-map-mode"></a>使用批注或映射模式

还可以更改滚动条的外观及其包含的其他功能。 例如，许多人喜欢在滚动条中包含*注释*，这提供了视觉提示，例如代码更改、断点、书签、错误和插入符号位置。

有些人喜欢使用*地图模式*，这会在滚动条上以缩图显示代码行。 在文件中有大量代码的开发人员可能会发现，映射模式比默认滚动条更有效地跟踪代码行。

有关如何更改滚动条的默认设置的详细信息，请参阅[自定义滚动条](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)页面。

## <a name="xaml-specific-features"></a>特定于 XAML 的功能

大多数以下功能在 Visual Studio IDE 中都是通用的，但其中一些功能为 XAML 开发人员简化了编码。

### <a name="xaml-code-snippets"></a>XAML 代码段

代码片段是可重复使用的代码块，你可以通过使用右键单击上下文菜单命令 "**插入代码片段**" 或键盘快捷方式（**ctrl** + **K**、 **ctrl** + **X**）的组合将其插入到代码文件中。 我们增强了[IntelliSense](../ide/using-intellisense.md) ，使其支持显示 XAML 代码段，这些代码段适用于内置代码段以及手动添加的任何自定义代码段。 一些现成的 XAML 代码段包括 `#region` 、 `Column definition` 、、 `Row definition` `Setter` 和 `Tag` 。

![在 IntelliSense 中显示 #region 选项的 XAML 代码编辑器](media/xaml-code-snippets.png "XAML 代码编辑器的屏幕截图，其中的 #region 选项显示在 IntelliSense 中")

有关详细信息，请参阅 "[代码片段](../ide/code-snippets.md)" 和 " [c # 代码片段](../ide/visual-csharp-code-snippets.md)" 页。

### <a name="xaml-region-support"></a>XAML #region 支持

从 Visual Studio 2015 开始，我们为 WPF 和 UWP 中的 XAML 开发人员提供 #region 支持，在[Xamarin](/xamarin/xamarin-forms/user-interface/text/editor/)中也是如此。 在 Visual Studio 2019 中，我们将继续对 #region 支持进行增量改进。 例如，在[版本 16.4](/visualstudio/releases/2019/release-notes-v16.4/)和更高版本中，#region 选项显示为开始键入 `<!` 。

![在 IntelliSense 中显示 #region 选项的 XAML 代码编辑器](media/code-editor-xaml-region.png "XAML 代码编辑器的屏幕截图，其中的 #region 选项显示在 IntelliSense 中")

如果要对你还需要展开或折叠的代码部分进行分组，则可以使用区域。

```xaml
    <!--#region NameOfRegion-->
    Your code is here
    <!--#endregion-->
```

有关区域的详细信息，请参阅[#region （c # 参考）](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region/)页。 有关展开和折叠代码段的详细信息，请参阅 "[大纲显示](../ide/outlining.md)" 页。

### <a name="xaml-comments"></a>XAML 注释

开发人员通常更倾向于使用注释来记录代码。 可以通过以下方式向**mainwindow.xaml**选项卡中的 xaml 代码添加注释：

- 在 `<!--` 注释之前输入，然后在 `-->` 注释之后添加。
- 输入 `<!` ，然后 `!--` 从选项列表中进行选择。

  ![XAML 代码编辑器右键单击 "添加注释" 对话框](media/xaml-code-editor-comments.png "右键单击上下文菜单的屏幕截图，用于在 XAML 代码编辑器中添加注释")

- 选择要用注释包围的代码，然后从 IDE 的工具栏中选择 "**注释**" 按钮。 若要撤消操作，请选择 "**取消注释**" 按钮。

  ![IDE 工具栏中的 "注释" 按钮和 "取消注释" 按钮](media/comment-undo-comment-buttons.png "IDE 工具栏中 "注释" 按钮和 "取消注释" 按钮的屏幕截图")

- 选择要用注释包围的代码，然后按**ctrl** + **K**， **ctrl** + **C**。 若要取消注释所选代码，请按**ctrl** + **K**， **ctrl** + **U**。

有关如何在**MainWindow.xaml.cs**选项卡中使用 c # 代码中的注释的详细信息，请参阅[文档注释](/dotnet/csharp/language-reference/language-specification/documentation-comments/)页面。

### <a name="xaml-lightbulbs"></a>XAML 灯泡

XAML 代码中显示的灯泡图标是可用于重构、生成或以其他方式修改代码的 "[快速操作](../ide/quick-actions.md)" 的一部分。

下面是几个示例，这些示例演示了如何利用 XAML 编码体验：

- **删除不必要的命名空间**。 在 XAML 代码编辑器中，不必要的命名空间以灰色文本显示。 如果将光标悬停在不必要的上，则会出现一个灯泡。 如果从下拉列表中选择 "**删除不必要的命名空间**" 选项，您将看到可以删除的预览。

  !["快速操作" 灯泡中的 XAML 代码编辑器的 "删除不必要的命名空间" 选项](media/xaml-code-editor-dimmed-namespaces-preview.png "XAML 代码编辑器的 "删除不必要的命名空间" 选项的屏幕截图，该选项使用 "快速操作" 灯泡显示")

- **重命名命名空间**。 此功能在突出显示某个命名空间后，可通过右键单击上下文菜单获得，使你可以轻松地一次更改一个设置的多个实例。 你还可以通过使用菜单栏，**编辑**  >  **重构**  >  **重命名**，或按**ctrl** + **r**，然后再次按**ctrl** + **R** r 来访问此功能。

  ![右键单击上下文菜单中的 XAML 代码编辑器的 "重命名命名空间" 选项](media/code-editor-rename-namespace.png "使用右键单击上下文菜单显示的 XAML 代码编辑器的 "重命名命名空间" 选项的屏幕截图")

  有关详细信息，请参阅[重命名代码符号重构](../ide/reference/rename.md)页。

### <a name="conditional-xaml-for-uwp"></a>UWP 的条件 XAML

条件 XAML 提供在 XAML 标记中使用 ApiInformation.IsApiContractPresent 方法的一种途径。 可以在 API 存在的情况下在标记中设置属性和实例化对象，无需使用代码隐藏。

有关详细信息，请参阅 "[条件 XAML](/windows/uwp/debug-test-perf/conditional-xaml/) " 页和 "[桌面应用（XAML 孤岛）" 页中的宿主 UWP XAML 控件](/windows/apps/desktop/modernize/xaml-islands/)。

### <a name="xaml-structure-visualizer"></a>XAML 结构可视化工具

代码编辑器中的结构可视化工具功能显示了结构参考线，它们是表示代码中的已打开和已关闭标记元素的垂直虚线。 这些垂直线使你可以更轻松地了解逻辑块开始和结束的位置。

有关详细信息，请参阅[导航代码](../ide/navigating-code.md)页。

### <a name="intellicode-for-xaml"></a>适用于 XAML 的 IntelliCode

将 XAML 标记添加到代码中时，通常以左尖括号开头 `<` 。 键入该尖括号时，将出现一个 IntelliCode 菜单，其中列出了几个比较流行的 XAML 标记。 选择要快速将其添加到代码中的一个。

您可以识别 IntelliCode 选择，因为它们显示在列表的顶部并且为带有星标。

![XAML 文本编辑器的 IntelliCode 列表](media/xaml-intellicode-selection.png "XAML 文本编辑器的 IntelliCode 列表的屏幕截图")

有关详细信息，请参阅 " [IntelliCode 概述](/visualstudio/intellicode/overview/)" 页。

### <a name="settings"></a>设置

有关 Visual Studio IDE 中的*所有*设置的详细信息，请参阅["代码编辑器](../ide/writing-code-in-the-code-and-text-editor.md)" 页的功能。

## <a name="xaml-optional-settings"></a>XAML 可选设置

您可以使用 "[选项](../ide/reference/options-dialog-box-visual-studio.md)" 对话框更改 XAML 代码编辑器的默认设置。 若要查看设置，请选择 "**工具**" "选项" "  >  **Options**  >  **文本编辑器**  >  **XAML**"。

![XAML 文本编辑器的选项列表](media/xaml-tools-options.png "XAML 文本编辑器选项列表的屏幕截图")

> [!NOTE]
> 还可以使用键盘快捷方式访问 "选项" 对话框。 下面是操作方法：按**Ctrl** + **Q**搜索 IDE，键入**选项**，然后按**enter**。 接下来，按**Ctrl** + **E**搜索 "选项" 对话框，键入 **"文本编辑器**"，按**enter**，键入**XAML**，然后按**enter**。
>  
> 有关键盘快捷方式的详细信息，请参阅[Visual Studio 的快捷提示](../ide/productivity-shortcuts.md#code-editor)页。

### <a name="universal-text-editor-options"></a>通用文本编辑器选项

在 XAML 的 "[选项](../ide/reference/options-text-editor-xaml-formatting.md)" 对话框中，以下前三个项通用于 VISUAL Studio IDE 支持的所有编程语言。 请访问下表中的链接信息，了解有关这些选项以及如何使用这些选项的详细信息。

|名称  |更多信息  |
|---------|---------|
|常规  | ["选项" 对话框：文本编辑器 > 所有语言](../ide/reference/options-text-editor-all-languages.md) |
|滚动栏 | [“选项”-&gt;“文本编辑器”-&gt;“所有语言”-&gt;“滚动条”](../ide/reference/options-text-editor-all-languages-scroll-bars.md) |
|制表符  |  [“选项”->“文本编辑器”->“所有语言”->“选项卡”](../ide/reference/options-text-editor-all-languages-tabs.md) |

### <a name="xaml-specific-text-editor-options"></a>特定于 XAML 的文本编辑器选项

下表列出了 "[选项](../ide/reference/options-text-editor-xaml-formatting.md)" 对话框中的设置，可在开发基于 XAML 的应用时增强编辑体验。 请访问链接的信息以了解有关这些选项以及如何使用这些选项的详细信息。

|名称  |更多信息  |
|---------|---------|
|格式化 | [选项，文本编辑器，XAML，格式](../ide/reference/options-text-editor-xaml-formatting.md) |
|杂项 |  [选项, 文本编辑器, XAML, 杂项](../ide/reference/options-text-editor-xaml-miscellaneous.md) |

> [!TIP]
> "**杂项**" 部分中的 "**大写事件处理程序方法名称**" 设置对 XAML 开发人员特别有用。 默认情况下，此设置处于*关闭状态*，因为它是新的，但我们建议将其设置为 *"开"* 以支持代码中的正确大小写。

## <a name="next-steps"></a>后续步骤

若要详细了解如何在调试模式下运行应用时实时编辑代码，请参阅[XAML 热重载](xaml-hot-reload.md)页。

## <a name="see-also"></a>另请参阅

- [Visual Studio 代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview/)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)
- [Xamarin 移动应用开发（Mac）](/visualstudio/mac/xamarin/)
- [Visual Studio 2019 for Mac-IDE 教程（Mac）](/visualstudio/mac/ide-tour/)
