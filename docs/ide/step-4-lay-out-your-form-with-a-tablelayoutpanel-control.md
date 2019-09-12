---
title: 步骤 4：使用 TableLayoutPanel 控件设置窗体布局
ms.date: 08/30/2019
ms.assetid: 61acde79-e115-4bad-bb06-1fbe37717a3e
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.devlang:
- csharp
- vb
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3595705030e2e969f99455700ab70f36bf22274a
ms.sourcegitcommit: 4dfe098ac0df294aad63e6b384d6575980798ca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70887981"
---
# <a name="step-4-lay-out-your-form-with-a-tablelayoutpanel-control"></a>步骤 4：使用 TableLayoutPanel 控件设置窗体布局

在此步骤中，向窗体添加一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件。 TableLayoutPanel 可帮助在窗体中正确地对齐你稍后将添加的控件。

## <a name="how-to-lay-out-your-form-with-a-tablelayoutpanel-control"></a>如何使用 TableLayoutPanel 控件设置窗体布局

1. 在 Visual Studio IDE 左侧，选择“工具箱”选项卡  。（或者，从菜单栏中选择“视图” > “工具箱”，或按“Ctrl+Alt+X”      。）

1. 选择“容器”组旁边的小三角形符号打开该组，如下面的屏幕截图所示  。

     ![容器组](../ide/media/express_toolbox.png)<br>
“容器”组 

1. 可以向窗体中添加类似按钮、复选框和标签这样的控件。 在“工具箱”中双击“TableLayoutPanel”  控件。 （您也可将控件从工具箱拖动到窗体上。）当执行此操作时，IDE 会将 TableLayoutPanel 控件添加到窗体中，如下面的屏幕截图所示。

     ![TableLayoutPanel 控件](../ide/media/express_formtablelayout.png)<br>
TableLayoutPanel 控件 

    > [!NOTE]
    > 添加 TableLayoutPanel 后，如果窗体中出现标题为“TableLayoutPanel 任务”的窗口，请选择窗体内的任何位置来关闭此窗口  。 在本教程后面部分，你将学习到有关此窗口的更多内容。

     请注意当选择“工具箱”  选项卡时工具箱是如何展开以覆盖窗体的，以及当选择工具箱外部的任何位置后它是如何关闭的。 这就是 IDE 中的自动隐藏功能。 通过选择窗口右上角的图钉图标在自动隐藏和就地锁定之间切换，你可为任何窗口启用或禁用此功能。 图钉图标如下所示。

     ![“图钉”图标](../ide/media/express_pushpintoolbox.png)<br>
“图钉”图标 

1. 通过选择“TableLayoutPanel”来确保将它选中。 可以通过查看“属性”窗口顶部的下拉列表来验证选定了哪个控件，如下面的屏幕截图所示  。

     ![显示 TableLayoutPanel 控件的“属性”窗口](../ide/media/express_controlspropwin.png)<br>
显示“TableLayoutPanel”控件的“属性”窗口   

1. 在“属性”窗口的工具栏上选择“按字母顺序”按钮   。 这会使“属性”窗口中的属性列表按字母顺序显示，这样更易于查找本教程中的属性  。

1. 控件选择器是“属性”窗口顶部的下拉列表  。 在此示例中，它显示选定了名为 `tableLayoutPanel1` 的控件。 可以通过在“Windows 窗体设计器”  中选择一个区域或者从控件选择器中进行选择来选择控件。

   选择 TableLayoutPanel 之后，请查找“Dock”  属性并选择“Dock”  ，此属性应设置为“无”  。 请注意，一个下拉箭头将出现在值旁边。 选择该箭头，然后选择“填充”按钮（中间的大按钮），如下面的屏幕截图所示  。

     ![选定“填充”的“属性”窗口](../ide/media/express_docktable.png)<br>
选定了“填充”的“属性”窗口   

     Visual Studio 中的停靠是指 IDE 中的一个窗口附加到另一个窗口或区域的情况  。 例如，“属性”窗口可以取消停靠，即在 Visual Studio 中独立地自由浮动，也可以靠近“解决方案资源管理器”停靠   。

1. 请注意，将 TableLayoutPanel 的“停靠”属性设置为“填充”后，此面板将填充整个窗体   。 如果再次调整窗体的大小，则 TableLayoutPanel 将保持停靠状态，并自行调整大小以适合窗体。

    > [!NOTE]
    > TableLayoutPanel 的工作方式类似于 Microsoft Office Word 中的表：它有行和列，并且单个单元格可以跨多个行和列。 每个单元格都可以存放一个控件（例如按钮、复选框或标签）。 TableLayoutPanel 将具有一个跨其整个顶部行的 <xref:System.Windows.Forms.PictureBox> 控件、一个位于其左下方单元格中的 <xref:System.Windows.Forms.CheckBox> 控件和四个位于其右下方单元格中的 <xref:System.Windows.Forms.Button> 控件。

1. TableLayoutPanel 当前具有两个大小相等的行和两个大小相等的列。 现在，我们来调整它们的大小，以使顶部行和右侧列更大一些。 在“Windows 窗体设计器”  中选择“TableLayoutPanel”。 在右上角有一个小的黑色三角形按钮，如下所示。

     ![“三角形”按钮](../ide/media/express_iconblacktriangle.gif)<br>
“三角形”按钮 

     此按钮指示该控件具有帮助你自动设置其属性的任务。

1. 选择三角形以显示控件的任务列表，如下面的屏幕截图所示。

     ![TableLayoutPanel 任务](../ide/media/express_tablepanel.png)<br>
“TableLayoutPanel”任务 

1. 选择“编辑行和列”任务，显示“列和行样式”窗口   。 选择“Column1”  ，确保选中“百分比”  按钮并在“百分比”  框中输入“15”  ，以将此控件的大小设置为 15%。 （这是一个 <xref:System.Windows.Forms.NumericUpDown> 控件，将在后面的教程中使用。）选择“Column2”并将其设置为 85%  。 先不要选择“确定”按钮，因为这将关闭此窗口  。 （但如果这样做，你可以使用任务列表重新打开它。）

     ![TableLayoutPanel 列和行样式](../ide/media/vs_tablelayoutpanel_setup.png)<br>
“TableLayoutPanel”列和行样式 

1. 从“列和行样式”窗口顶部的“显示”下拉列表中选择“行”    。 将“Row1”设置为 90% 并将“Row2”设置为 10%   。

1. 选择“确定”  按钮。 现在，TableLayoutPanel 应具有一个大的顶部行、一个小的底部行、一个小的左侧列和一个大的右侧列。 （可在 TableLayoutPanel 中调整行和列的大小，方法是在窗体中选择“tableLayoutPanel1”，然后拖动其行和列边框  。）

     ![具有已调整大小的 TableLayoutPanel 的 Form1](../ide/media/vs_formafterlayoutpanel.png)<br>
具有已调整大小的“TableLayoutPanel”的“Form1”（图片查看器）  

## <a name="next-steps"></a>后续步骤

* 要转到下一个教程步骤，请参阅[步骤 5：向窗体添加控件](../ide/step-5-add-controls-to-your-form.md)  。

* 要返回上一个教程步骤，请参阅[步骤 3：设置窗体属性](../ide/step-3-set-your-form-properties.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
