---
title: 步骤 5：向窗体添加控件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: dc2746f4-0b5c-4674-9ef7-f40f94150f52
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 89ca4c02a1cbb1171619060b9478b5f2d3ccaa36
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295718"
---
# <a name="step-5-add-controls-to-your-form"></a>步骤 5：向窗体添加控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在此步骤中，将向窗体添加控件（如 `PictureBox` 控件和 `CheckBox` 控件）。 然后向窗体添加按钮。

 ![link to video](../data-tools/media/playvideo.gif "PlayVideo")For a video version of this topic, see [Tutorial 1: Create a Picture Viewer in Visual Basic - Video 2](https://go.microsoft.com/fwlink/?LinkId=205211) or [Tutorial 1: Create a Picture Viewer in C# - Video 2](https://go.microsoft.com/fwlink/?LinkId=205200). 这些视频使用 Visual Studio 的早期版本，因此在一些菜单命令和其他用户界面元素上略有差异。 但是，概念和过程与当前版本的 Visual Studio 大同小异。

### <a name="to-add-controls-to-your-form"></a>向窗体添加控件

1. 转到“工具箱”选项卡（位于 Visual Studio IDE 左侧），并展开“公共控件”组。 这将显示窗体上最常见的控件。

2. 选择窗体上的 TableLayoutPanel 控件。 若要验证是否已选中 TableLayoutPanel，请确保其名称显示在“属性”窗口顶部的下拉列表框中。 你也可使用“属性”窗口顶部的下拉列表框来选择窗体控件。 用此方法选择控件通常要比用鼠标选择小控件更容易。

3. 双击“PictureBox”项，将 PictureBox 控件添加到窗体。 由于已停靠 TableLayoutPanel 来填充您的窗体，因此 IDE 会将 PictureBox 控件添加到第一个空单元格（左上角）。

4. 如下图所示，选择新的 PictureBox 控件以将其选中，然后选择新 PictureBox 控件上的黑色三角形以显示其任务列表。

     ![PictureBox tasks](../ide/media/express-pictureboxtasks.png "Express_PictureBoxTasks") PictureBox tasks

    > [!NOTE]
    > 如果误将错误类型的控件添加到 TableLayoutPanel 中，可删除该控件。 右键单击该控件，然后选择其上下文菜单上的“删除”。 也可使用菜单栏从窗体中删除控件。 在菜单栏上，依次选择“编辑”、“撤消”或“编辑”、“删除”。

5. 选择“在父容器中停靠”链接。 这会自动将 PictureBox 的“Dock”属性设置为“Fill”。 为此，请选择 PictureBox 控件以将其选中，然后转到“属性”窗口，确保将“Dock”属性设置为“Fill”。

6. 更改 PictureBox 的“ColumnSpan”属性，使 PictureBox 跨两个列。 选择 PictureBox 控件并将其“ColumnSpan”属性设置为“2”。 此外，当 PictureBox 为空时，您需要显示一个空框架。 将其“BorderStyle”属性设置为“Fixed3D”。

    > [!NOTE]
    > 如果未看到 PictureBox 的“ColumnSpan”属性，表明可能已将 PictureBox 添加到窗体而不是 TableLayoutPanel。 若要修复此问题，请选择 PictureBox 并将其删除，然后选择 TableLayoutPanel，再添加新的 PictureBox。

7. 选择窗体上的 TableLayoutPanel，然后将“CheckBox”控件添加到窗体。 双击工具箱中的“CheckBox”项，向表中下一个空白单元格添加新的 CheckBox 控件。 由于 PictureBox 占据了 TableLayoutPanel 中的前两个单元格，因此 CheckBox 控件将添加到左下方的单元格。 如下图所示，选择“Text”属性并键入单词“Stretch”。

     ![TextBox control with Stretch property](../ide/media/express-pictureviewercheckbox.png "Express_PictureViewerCheckbox") TextBox control with Stretch property

8. 选择窗体上的 TableLayoutPanel，然后转到工具箱（可在此获取 TableLayoutPanel 控件）中的“容器”组，并双击“FlowLayoutPanel”项以将一个新控件添加到 PictureBox 的最后一个单元格（右下方）。 然后，在 TableLayoutPanel 中停靠 FlowLayoutPanel（方法是选择 FlowLayoutPanel 的黑色三角形任务列表中的“在父容器中停靠”，或将 FlowLayoutPanel 的“Dock”属性设置为“Fill”）。

    > [!NOTE]
    > FlowLayoutPanel 是一个容器，它将其他控件按顺序排列在行中。 在调整 FlowLayoutPanel 的大小时，如果 FlowLayoutPanel 的空间允许将其所有控件置于单个行中，则它会执行此操作。 否则，它会将这些控件依次排列到多个行中（一个行位于另一个行的上方）。 将使用 FlowLayoutPanel 来容纳四个按钮。 如果按钮按照一个叠一个的顺序添加，请确保在添加按钮前选择 FlowLayoutPanel。 尽管之前提到每个单元格只能存放一个控件，但是 TableLayoutPanel 的右下角单元格中具有四个按钮控件。 这是因为您可以在单元格中放入一个可存放其他控件的控件。 这种控件称为容器，FlowLayoutPanel 即是一个容器。

### <a name="to-add-buttons"></a>添加按钮

1. 选择新添加的 FlowLayoutPanel。 转到工具箱中的“公共控件”，然后双击“按钮”项以将一个名为“button1”的按钮控件添加到 FlowLayoutPanel。 重复上述操作以添加另一个按钮。 IDE 确定已存在名为“button1”的按钮，并会将下一个按钮命名为“button2”。

2. 通常，使用工具箱来添加其他按钮。 这一次，请选择“button2”，然后在菜单栏上选择“编辑”、“复制”（或按 Ctrl+C）。 在菜单栏上，选择“编辑”、“粘贴”（或按 Ctrl+V）以粘贴按钮的副本。 此时再次粘贴该副本。 IDE 此时已将“button3”和“button4”添加到 FlowLayoutPanel。

    > [!NOTE]
    > 可以复制并粘贴任何控件。 IDE 以逻辑方式命名和放置新的控件。 如果将一个控件粘贴到容器中，则 IDE 将选择下一个逻辑放置空间。

3. 选择第一个按钮，并将其“Text”属性设置为“显示图片”。 然后分别将后面三个按钮的“Text”属性设置为“清除图片”、“设置背景色”和“关闭”。

4. 下一步是调整这些按钮的大小并进行排列，使它们与面板的右侧对齐。 选择 FlowLayoutPanel 并查看其“FlowDirection”属性。 将该属性更改为“RightToLeft”。 一旦执行此操作，这些按钮会自行与单元格的右侧对齐，并颠倒其顺序，以使“显示图片”按钮位于右侧。

    > [!NOTE]
    > 如果这些按钮的顺序仍是错误的，则可以将这些按钮在 FlowLayoutPanel 中四处拖动以按任意顺序重新排列它们。 可选择一个按钮并将其向左或向右拖动。

5. 选择“关闭”按钮以将其选中。 按住 Ctrl 键并选择其他三个按钮，以便将其全部选中。 在选定所有这些按钮后，转到“属性”窗口，然后向上滚动到“AutoSize”属性。 此属性会告知按钮自动调整自身大小以适合其所有文本。 将此属性设置为“true”。 此时这些按钮应具有适当大小且按照适当的顺序排列。 (As long as all four buttons are selected, you can change all four **AutoSize** properties at the same time.) The following picture shows the four buttons.

     ![Picture Viewer with four buttons](../ide/media/express-autosize.png "Express_AutoSize") Picture Viewer with four buttons

6. 此时重新运行程序以查看具有最新布局的窗体。 选择这些按钮和选中复选框并不会执行任何操作，但它们很快将会起作用。

### <a name="to-continue-or-review"></a>继续或查看

- 若要转到下一个教程，请参阅[步骤 6：命名按钮控件](../ide/step-6-name-your-button-controls.md)。

- 若要返回上一个教程，请参阅[步骤 4：使用 TableLayoutPanel 控件设置窗体的布局](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)。
