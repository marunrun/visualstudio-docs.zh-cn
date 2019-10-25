---
title: Windows 窗体设计器教程
ms.date: 08/09/2019
ms.topic: conceptual
helpviewer_keywords:
- Windows Forms Designer, get started
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 419e5ddb5d915307130a6fdadd795ce5b3236033
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72634136"
---
# <a name="walkthrough-get-started-with-windows-forms-designer"></a>演练：Windows 窗体设计器入门

Windows 窗体设计器提供了许多用于生成 Windows 窗体应用程序的工具。 本文说明如何使用设计器提供的各种工具生成应用，包括以下任务：

- 使用对齐线排列控件。
- 使用智能标记完成设计器任务。
- 设置控件的边距和填充。
- 使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件排列控件。
- 使用 <xref:System.Windows.Forms.SplitContainer> 控件对控件的布局进行分区。
- 通过“文档大纲”窗口导航布局。
- 显示大小和位置信息的位置控件。
- 使用“属性”窗口设置属性值。

完成后，你将拥有一个使用 Windows窗体设计器中提供的多种布局功能组装而成的自定义控件。 此控件可实现简单计算器的用户界面 (UI)。 下图显示了计算器控件的一般布局：

![指导教程“计算器”的用户界面](media/calculator-ui.gif)

## <a name="create-the-custom-control-project"></a>创建自定义控件项目

第一步是创建 DemoCalculator 控件项目。

1. 在 Visual Studio 中，创建新的“Windows 窗体控件库”项目  。 将项目命名为 DemoCalculatorLib  。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的 Windows 窗体控件库模板](media/windows-forms-control-library-template.png)

   ::: moniker-end

2. 若要重命名文件，请在“解决方案资源管理器”中，右键选择“UserControl1.vb”或“UserControl1.cs”，选择“重命名”并将文件名更改为 DemoCalculator.vb 或 DemoCalculator.cs     。 当系统询问是否重命名对代码元素“UserControl1”的所有引用时，选择“是”  。

Windows 窗体设计器显示 DemoCalculator 控件的设计器图面。 在此视图中，可以通过从“工具箱”中选择控件和组件，并将其置于设计器图面，来以图形方式设计控件的外观。 有关自定义控件的详细信息，请参阅[各种自定义控件](/dotnet/framework/winforms/controls/varieties-of-custom-controls)。

## <a name="design-the-control-layout"></a>设计控件布局

DemoCalculator 控件包含多个 Windows 窗体控件。 在此过程中，将使用 Windows 窗体设计器来排列控件。

1. 在 Windows 窗体设计器中，通过选择右下角的尺寸控点并将其向下和向右拖动，将 DemoCalculator 控件更改为更大大小。 在 Visual Studio 的右下角，查找控件的大小和位置信息。 通过在调整控件大小时观察大小信息，将控件的大小设置为宽度 500 和高度 400。

2. 在“工具箱”中，选择“容器”节点以将其打开   。 选择 SplitContainer 控件并将其拖动到设计器图面  。

   随即会将 `SplitContainer` 置于 DemoCalculator 控件的设计器图面。

    > [!TIP]
    > `SplitContainer` 控件自行调整大小以适应 DemoCalculator 控件的大小。 查看“属性”窗口以查看 `SplitContainer` 控件的属性设置  。 查找 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性。 其值为 [DockStyle.Fill](xref:System.Windows.Forms.DockStyle.Fill)，这意味着 `SplitContainer` 控件会始终自行将其大小调整为 DemoCalculator 控件的边界。 重设 DemoCalculator 控件的大小以验证此行为。

3. 在“属性”  窗口中，将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性的值更改为 `None`。

    `SplitContainer` 控件收缩为其默认大小，不再遵循 DemoCalculator 控件的大小。

4. 选择 `SplitContainer` 控件右上角的智能标记字形（![智能标记字形](media/smart-tag-glyph.gif)）。 选择“在父容器中停靠”  以将 `Dock` 属性设置为 `Fill`。

    `SplitContainer` 控件停靠到 DemoCalculator 控件的边界。

    > [!NOTE]
    > 多个控件提供智能标记以便于设计。 有关详细信息，请参见[演练：使用 Windows 窗体控件上的智能标记执行常规任务](/dotnet/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls)。

5. 选择面板之间的垂直边框，并将其拖到右侧，以便让左面板占据大部分空间。

    `SplitContainer` 将 DemoCalculator 控件分为两个面板，其中包含一个用于分隔它们的可移动边框。 左面板将保留计算器按钮和显示，右面板将显示用户执行的算术运算的记录。

6. 在“属性”  窗口中，将 `BorderStyle` 属性的值更改为 `Fixed3D`。

7. 在“工具箱”中，选择“公共控件”节点以将其打开   。 选择 `ListView` 控件并将其拖动到 `SplitContainer` 控件的右面板。

8. 选择 `ListView` 控件的智能标记字形。 在智能标记面板中，将 `View` 设置更改为 `Details`。

9. 在智能标记面板中，选择“编辑列”  。

   “ColumnHeader 集合编辑器”  对话框随即打开。

10. 在“ColumnHeader 集合编辑器”  对话框中，选择“添加”  以将列添加到 `ListView` 控件。 将列的 `Text` 属性值更改为“历史记录”  。 选择“确定”  以创建列。

11. 在智能标记面板中，选择“在父容器中停靠”  ，然后选择智能标记字形来关闭智能标记面板。

12. 从“容器”  节点**工具箱**，将 `TableLayoutPanel` 控件拖动到 `SplitContainer` 控件的左面板中。

    `TableLayoutPanel` 控件显示在设计器图面上，并打开其智能标记面板。 `TableLayoutPanel` 控件在网格中排列其子控件。 `TableLayoutPanel` 控件将保留 DemoCalculator 控件的显示和按钮。 有关详细信息，请参见[演练：使用 TableLayoutPanel 排列控件](/dotnet/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel)。

13. 选择智能标记面板上的“编辑行和列”  。

    随即将打开“列和行样式”  对话框。

14. 选择“添加”按钮  ，直到显示五列。 选择所有五列，然后在“大小类型”框中选择“百分比”   。 将“百分比”值设置为“20”   。 这会将每列设置为相同宽度。

15. 在“显示”下，选择“行”   。

16. 选择“添加”  ，直到显示五行。 选择所有五行，然后在“大小类型”框中选择“百分比”   。 将“百分比”值设置为“20”   。 这会将每行设置为相同高度。

17. 选择“确定”  接受更改，然后选择智能标记字形以关闭智能标记面板。

18. 在“属性”  窗口中，将 `Dock` 属性的值更改为 `Fill`。

## <a name="populate-the-control"></a>填充控件

现在，已设置控件的布局，可以使用按钮和显示填充 DemoCalculator 控件。

1. 在“工具箱”  中，双击 `TextBox` 控件图标。

   将 `TextBox` 控件置于 `TableLayoutPanel` 控件的第一个单元格中。

2. 在“属性”  窗口中，将 `TextBox` 控件的 ColumnSpan 属性的值更改为“5”  。

   `TextBox` 控件会移动到该行的居中位置。

3. 将 `TextBox` 控件的 `Anchor` 属性值更改为 `Left``Right`。

   `TextBox` 控件将水平扩展以跨越所有五列。

4. 将 `TextBox` 控件的 `TextAlign` 属性值更改为 `Right`。

5. 在“属性”  窗口中，展开 `Font` 属性节点。 将 `TextBox` 控件的 `Size` 设置为“14”  ，并将 `Bold` 设置为“true”  。

6. 选择 `TableLayoutPanel` 控件。

7. 在“工具箱”  中，双击 `Button` 图标。

   将 `Button` 控件置于 `TableLayoutPanel` 控件的下一个打开单元格中。

8. 在“工具箱”  中，双击 `Button` 图标四次以填充 `TableLayoutPanel` 控件的第二行。

9. 在按住 Shift  键的同时选择所有五个 `Button` 控件，来选中这些控件。 按 Ctrl  +C  将 `Button` 控件复制到剪贴板。

10. 按 Ctrl  +V  三次将 `Button` 控件的副本粘贴到 `TableLayoutPanel` 控件的其余行中。

11. 在按住 Shift  键的同时选择所有 20 个 `Button` 控件，来选中这些控件。

12. 在“属性”  窗口中，将 `Dock` 属性的值更改为 `Fill`。

    所有 `Button` 控件均停靠以填充其包含的单元格。

13. 在“属性”  窗口中，展开 `Margin` 属性节点。 将 `All` 的值设置为“5”  。

    将所有 `Button` 控件的大小都设置为较小，以便在它们之间创建更大的边距。

14. 选择“button10”  和“button20”  ，然后按“删除”  以将其从布局中删除。

15. 选择“button5”  和“button15”  ，然后将其 `RowSpan` 属性的值更改为“2”  。 这些将成为 DemoCalculator 控件的“清除”  和 =  按钮。

## <a name="use-the-document-outline-window"></a>使用“文档大纲”窗口

当通过多个控件填充控件或窗体时，可能会发现使用“文档大纲”窗口导航布局更容易。

1. 在菜单栏上选择“查看”   >   “其他窗口” >   “文档大纲”。

   “文档大纲”窗口显示 DemoCalculator 控件及其构成控件的树视图。 `SplitContainer` 等容器控件将其子控件显示为树中的子节点。 还可以使用“文档大纲”窗口重命名控件。

2. 在“文档大纲”  窗口中，右键选择“button1”  ，然后选择“重命名”  。 将其名称更改为 sevenButton。

3. 使用“文档大纲”  窗口，根据以下列表将 `Button` 控件的名称从设计器生成的名称重命名为生产名称：

   - 将 button1 重命名为“sevenButton” 

   - 将 button2 重命名为“eightButton” 

   - 将 button3 重命名为“nineButton” 

   - 将 button4 重命名为“divisionButton” 

   - 将 button5 重命名为“clearButton” 

   - 将 button6 重命名为“fourButton” 

   - 将 button7 重命名为“fiveButton” 

   - 将 button8 重命名为“sixButton” 

   - 将 button9 重命名为“multiplicationButton” 

   - 将 button11 重命名为“oneButton” 

   - 将 button12 重命名为“twoButton” 

   - 将 button13 重命名为“threeButton” 

   - 将 button14 重命名为“subtractionButton” 

   - 将 button15 重命名为“equalsButton” 

   - 将 button16 重命名为“zeroButton” 

   - 将 button17 重命名为“changeSignButton” 

   - 将 button18 重命名为“decimalButton” 

   - 将 button19 重命名为“additionButton” 

4. 使用“文档大纲”  和“属性”  窗口，根据以下列表更改每个 `Button` 控件名称的 `Text` 属性值：

   - 将 sevenButton 控件文本属性更改为“7” 

   - 将 eightButton 控件文本属性更改为“8” 

   - 将 nineButton 控件文本属性更改为“9” 

   - 将 divisionButton 控件文本属性更改为“/”  （正斜杠）

   - 将 clearButton 控件文本属性更改为“Clear” 

   - 将 fourButton 控件文本属性更改为“4” 

   - 将 fiveButton 控件文本属性更改为“5” 

   - 将 sixButton 控件文本属性更改为“6” 

   - 将 multiplicationButton 控件文本属性更改为“\*”  （星号）

   - 将 oneButton 控件文本属性更改为“1” 

   - 将 twoButton 控件文本属性更改为“2” 

   - 将 threeButton 控件文本属性更改为“3” 

   - 将 subtractionButton 控件文本属性更改为“-”  （连字符）

   - 将 equalsButton 控件文本属性更改为“=”  （等于号）

   - 将 zeroButton 控件文本属性更改为“0” 

   - 将 changeSignButton 控件文本属性更改为“+/-” 

   - 将 decimalButton 控件文本属性更改为“.”  （句点）

   - 将 additionButton 控件文本属性更改为“+”  （加号）

5. 在设计器图面上，通过在按住 Shift  键的同时选择所有 `Button` 控件来选中它们。

6. 在“属性”  窗口中，展开 `Font` 属性节点。 将所有 `Button` 控件的 `Size` 设置为“14”  ，并将 `Bold` 设置为“true”  。

这就完成了 DemoCalculator 控件的设计。 剩下的工作就是提供计算器逻辑。

## <a name="implement-event-handlers"></a>实现事件处理程序

DemoCalculator 控件上的按钮具有可用于实现大部分计算器逻辑的事件处理程序。 借助 Windows 窗体设计器，只需双击一次即可为所有按钮实现所有事件处理程序的存根。

1. 在设计器图面上，通过在按住 Shift  键的同时选择所有 `Button` 控件来选中它们。

2. 双击其中一个 `Button` 控件。

   由设计器生成的事件处理程序将打开“代码编辑器”。

## <a name="test-the-control"></a>测试控件

因为 DemoCalculator 控件继承自 <xref:System.Windows.Forms.UserControl> 类，所以可以使用 UserControl 测试容器  对其行为进行测试。 有关详细信息，请参阅[如何：测试 UserControl 的运行时行为](/dotnet/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol)。

1. 按 F5  生成并运行 UserControl 测试容器  中的 DemoCalculator 控件。

2. 选择 `SplitContainer` 面板之间的边框，并向左和向右拖动它。 `TableLayoutPanel` 及其所有子控件会自行重设大小以适应可用空间。

3. 完成控件测试后，选择“关闭”  。

## <a name="use-the-control-on-a-form"></a>在窗体上使用控件

DemoCalculator 控件可在其他复合控件或窗体上使用。 以下过程介绍如何使用它。

### <a name="create-the-project"></a>创建项目

第一步是创建应用程序项目。 将使用此项目生成显示自定义控件的应用程序。

1. 创建新的“Windows 窗体应用程序”  项目，并将其命名为“DemoCalculatorTest”  。

2. 在“解决方案资源管理器”  中，右键单击“DemoCalculatorTest”  项目，然后选择“添加引用”  以打开“添加引用”  对话框。

3. 选择“项目”  选项卡，然后双击 DemoCalculatorLib 项目以将引用添加到测试项目。

4. 在“解决方案资源管理器”  中，右键单击“DemoCalculatorTest”  ，然后选择“设置为启动项目”  。

5. 在 Windows 窗体设计器中，将窗体的大小增加为约 700 x 500  。

### <a name="use-the-control-in-the-forms-layout"></a>在窗体的布局中使用控件

若要在应用程序中使用 DemoCalculator 控件，需要将其置于窗体之上。

1. 在“工具箱”  中，展开“DemoCalculatorLib 组件”  节点。

2. 将 DemoCalculator  控件从“工具箱”  拖动到窗体。 将控件移动到窗体的左上角。 当控件接近窗体边框时，将显示对齐线  。 对齐线指示窗体的 `Padding` 属性和控件的 `Margin` 属性的距离。 将控件置于对齐线指示的位置。

   有关详细信息，请参见[演练：使用对齐线排列控件](/dotnet/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines)。

3. 将 `Button` 控件从“工具箱”  拖放到窗体。

4. 围绕 DemoCalculator 控件移动 `Button` 控件，并观察对齐线的显示位置。 可以使用此功能精确而轻松地对齐控件。 完成后，删除 `Button` 控件。

5. 右键选择 DemoCalculator 控件，然后选择“属性”  。

6. 将 `Dock` 属性的值更改为 `Fill`。

7. 选择窗体，然后展开 `Padding` 属性节点。 将“All”  的值更改为“20”  。

   减小 DemoCalculator 控件的大小以容纳窗体的新 `Padding` 值。

8. 通过将各种尺寸控点拖动到不同位置来重设窗体大小。 观察 DemoCalculator 控件如何重设大小以适应。

## <a name="next-steps"></a>后续步骤

本文演示了如何构造用于简单计算器的用户界面。 若要继续，可以通过实现计算器逻辑来扩展其功能，然后[使用 ClickOnce 发布应用](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。 或者，继续学习[使用 Windows 窗体创建图片查看器](../ide/tutorial-1-create-a-picture-viewer.md)的其他教程。

## <a name="see-also"></a>请参阅

- [Windows 窗体控件](/dotnet/framework/winforms/controls/)
- [Windows 窗体控件的辅助功能](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)
- [使用 ClickOnce 发布](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)