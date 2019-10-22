---
title: 步骤 5：向窗体添加控件
ms.date: 08/30/2019
ms.assetid: dc2746f4-0b5c-4674-9ef7-f40f94150f52
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b88af1a0ac1ec51f57d3aa339c2c2ec4adb45134
ms.sourcegitcommit: 6eed0372976c0167b9a6d42ba443f9a474b8bb91
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2019
ms.locfileid: "71119003"
---
# <a name="step-5-add-controls-to-your-form"></a>步骤 5：向窗体添加控件

在此步骤中，将向窗体添加控件（如 <xref:System.Windows.Forms.PictureBox> 控件和 <xref:System.Windows.Forms.CheckBox> 控件）。 然后向窗体添加 <xref:System.Windows.Forms.Button> 控件。

## <a name="how-to-add-controls-to-your-form"></a>如何向窗体添加控件

1. 选择 Visual Studio IDE 左侧的“工具箱”选项卡（或按“Ctrl+Alt+X”），然后展开“常用控件”组      。 这将显示窗体上最常见的控件。

1. 双击“PictureBox”项，将 PictureBox 控件添加到窗体。  由于已停靠 TableLayoutPanel 来填充您的窗体，因此 IDE 会将 PictureBox 控件添加到第一个空单元格（左上角）。

1. 如下面的屏幕截图所示，选择新的“PictureBox”控件将其选中，然后选择新 PictureBox 控件上的黑色三角形以显示其任务列表  。

    ![PictureBox 任务](../ide/media/express_pictureboxtasks.png)<br/>“PictureBox”任务  *

    > [!NOTE]
    > 如果误将错误类型的控件添加到 TableLayoutPanel 中，可删除该控件。 右键单击该控件，然后选择其上下文菜单上的“删除”。  也可使用菜单栏从窗体中删除控件。 在菜单栏上，依次选择“编辑”   > “撤消”  或“编辑”   > “删除”  。

1. 在“PictureBox”控件的“PictureBox 任务”菜单中，选择“停靠在父容器中”链接    。 这会自动将 PictureBox 的“Dock”属性设置为“Fill”。   为此，请选择 PictureBox  控件以将其选中，然后转到“属性”  窗口，确保将“Dock”  属性设置为“Fill”  。

1. 更改 PictureBox 的“ColumnSpan”属性，使 PictureBox 跨两个列。  在“PictureBox”中，选择“PictureBox”控件并将其“ColumnSpan”属性设置为“2”     。 此外，当 PictureBox 为空时，您需要显示一个空框架。 将其“BorderStyle”属性设置为“Fixed3D”。  

    > [!NOTE]
    > 如果未看到 PictureBox 的“ColumnSpan”属性，表明可能已将 PictureBox 添加到窗体而不是 TableLayoutPanel。  若要修复此问题，请选择“PictureBox”  并将其删除，然后选择“TableLayoutPanel”  ，再添加新的“PictureBox”。

1. 选择窗体上的“TableLayoutPanel”  ，然后将“CheckBox”控件添加到窗体。 双击“工具箱”  中的“CheckBox”  项，向表中下一个空白单元格添加新的 CheckBox 控件。 由于 PictureBox 占据了 TableLayoutPanel 中的前两个单元格，因此 CheckBox 控件将添加到左下方的单元格。 如下图所示，选择“文本”属性并键入单词“Stretch”   。

    ![带 Stretch 属性的 TextBox 控件](../ide/media/express_pictureviewercheckbox.png)<br/>带 Stretch 属性  的 TextBox 控件 

1. 选择窗体上的“TableLayoutPanel”，然后转到“工具箱”（可在此获取“TableLayoutPanel”控件）中的“容器”组，并双击“FlowLayoutPanel”项以将一个新控件添加到最后一个单元格（右下方）     。 然后，将 FlowLayoutPanel 停靠在 TableLayoutPanel 中。 要实现此操作，请选择 FlowLayoutPanel 的黑色三角形任务列表中的“停靠在父容器中”，或将 FlowLayoutPanel 的“停靠”属性设置为“填充”    。

    > [!NOTE]
    > <xref:System.Windows.Forms.FlowLayoutPanel> 是一个容器，它将其他控件按顺序排列在一行中。 在调整 FlowLayoutPanel 的大小时，如果 FlowLayoutPanel 的空间允许将其所有控件置于一行中，则它会执行此操作。 否则，它会将这些控件依次排列到多个行中（一个行位于另一个行的上方）。 <br/><br/>在这里，你将使用 FlowLayoutPanel 来包含四个按钮。 添加按钮时，如果要使按钮按顺序排列，请确保在添加按钮前选择 FlowLayoutPanel。 <br/><br/>（通常，每个单元只包含一个控件。 在本例中，TableLayoutPanel 的右下角单元包含四个按钮控件。 为什么？  这是因为 FlowLayoutPanel 是一个容器控件，这种控件的单元格中可以包含其他控件。）

## <a name="to-add-buttons"></a>添加按钮

1. 选择新添加的 FlowLayoutPanel。 转到“工具箱”  中的“公共控件”  ，然后双击“按钮”  项以将一个名为“button1”  的按钮控件添加到 FlowLayoutPanel。 重复上述操作以添加另一个按钮。 IDE 确定已存在名为“button1”的按钮，并会将下一个按钮命名为“button2”。  

1. 通常情况下，你会使用“工具箱”来添加其他按钮  。 这一次，请选择“button2”，然后在菜单栏上选择“编辑” > “复制”（或按“Ctrl+C”）      。 接下来，在菜单栏上，选择“编辑” > “粘贴”（或按“Ctrl+V”）以粘贴按钮的副本     。 此时再次粘贴该副本。 请注意，IDE 会将“button3”和“button4”添加到 FlowLayoutPanel   。

    > [!NOTE]
    > 可以复制并粘贴任何控件。 IDE 以逻辑方式命名和放置新的控件。 如果将一个控件粘贴到容器中，则 IDE 将选择下一个逻辑放置空间。

1. 选择第一个按钮，并将其“Text”属性设置为“显示图片”。   然后分别将后面三个按钮的“Text”属性设置为“清除图片”、“设置背景色”和“关闭”。    

1. 现在，我们来调整这些按钮的大小并进行排列，使它们与面板的右侧对齐。 选择“FlowLayoutPanel”  并查看其“FlowDirection”  属性。 将该属性更改为“RightToLeft”。 

   这些按钮会自行与单元格的右侧对齐，并颠倒其顺序，以使“显示图片”按钮位于右侧  。

    > [!NOTE]
    > 如果这些按钮的顺序仍是错误的，则可以将这些按钮在 FlowLayoutPanel 中四处拖动以按任意顺序重新排列它们。 可选择一个按钮并将其向左或向右拖动。

1. 选择“关闭”按钮以将其选中。  然后，要同时选择其余按钮，请在按住 Ctrl 键的同时选择它们  。

   选定所有按钮后，转到“属性”窗口，然后向上滚动到“自动调整大小”属性   。 此属性会告知按钮自动调整自身大小以适合其所有文本。 将此属性设置为“True”  。

   此时这些按钮应具有适当大小且按照适当的顺序排列。 （只要选定所有四个按钮，就可以同时更改所有四个“AutoSize”属性。）  下图显示了这四个按钮。

    ![带四个按钮的图片查看器](../ide/media/express_autosize.png)<br/>带四个按钮的图片查看器 

1. 现在，再次运行程序以查看更改。

   请注意，这些按钮和复选框并不执行任何操作，但很快会执行。

## <a name="to-continue-or-review"></a>继续或查看

* 要转到下一个教程步骤，请参阅[步骤 6：  命名按钮控件](../ide/step-6-name-your-button-controls.md)。

* 要返回上一个教程步骤，请参阅[步骤 4：使用 TableLayoutPanel 控件设置窗体布局](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
