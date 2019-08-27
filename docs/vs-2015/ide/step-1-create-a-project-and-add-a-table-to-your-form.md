---
title: 步骤 1：创建项目并向窗体添加表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 1cac4ba4-f3cd-43bd-ad5d-50fc599234e8
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 807d2b7de34acda52dd05ff8263ae3303dca61c6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441920"
---
# <a name="step-1-create-a-project-and-add-a-table-to-your-form"></a>步骤 1：创建项目并向窗体添加表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建匹配游戏的第一步是创建项目并向窗体添加表。 该表有助于将图标对齐到有序的 4x4 网格。 你还要设置若干属性，以改善游戏板的外观。  
  
### <a name="to-create-a-project-and-add-a-table-to-your-form"></a>创建项目并向窗体添加表  
  
1. 在菜单栏上，依次选择“文件” 、“新建” 、“项目” 。  
  
2. 如果你不使用 Visual Studio Express，则需要先选择一种编程语言。 在“已安装的模板”列表中选择“Visual C#”或“Visual Basic”。  
  
3. 在项目模板列表中，选择“Windows 窗体应用程序”，将该项目命名为“MatchingGame”，然后选择“确定”按钮。  
  
4. 在“属性”窗口中，设置下列窗体属性。  
  
   1. 将窗体的“Text”属性从“Form1”更改为“Matching Game”。 该文本显示在游戏窗口的顶部。  
  
   2. 将窗体大小设置为 550 像素（宽）× 550 像素（高）。 设置方法有两种：将“Size”属性设置为“550, 550”；或者拖拽窗体的边角，直至你在集成开发环境 (IDE) 的右下角看到正确大小。  
  
5. 通过选择 IDE 左侧的“工具箱”选项卡显示工具箱。  
  
6. 从工具箱中的“容器”类别拖动一个 `TableLayoutPanel` 控件，然后为其设置以下属性。  
  
   1. 将“BackColor”属性设置为“CornflowerBlue”。 为此，请通过选择“属性”窗口中“BackColor”属性旁边的下拉箭头，打开“BackColor”对话框。  然后，选择“BackColor”对话框中的“Web”选项卡，查看可用颜色名称的列表。  
  
      > [!NOTE]
      > 这些颜色未按字母顺序排列，CornflowerBlue 位于列表底部附近。  
  
   2. 通过选择“Dock”属性旁边的下拉按钮并选择大的中间按钮，将该属性设置为“Fill”。 这会扩展该表，使其覆盖整个窗体。  
  
   3. 将“CellBorderStyle”属性设置为“Inset”。 这会在游戏板上每个单元格之间提供可视边框。  
  
   4. 选择 TableLayoutPanel 右上角的三角形按钮，以显示任务菜单。  
  
   5. 在任务菜单上，选择“添加行”两次以再添加两行，然后选择“添加列”两次以再添加两列。  
  
   6. 在任务菜单上，选择“编辑行和列”，打开“列和行样式”窗口。 选择每一列，再选择“百分比”选项按钮，然后将每列的宽度设置为总宽度的 25%。 然后从窗口顶部的下拉框选择“行”，并将每个行的高度设置为 25%。 完成后，选择“确定”按钮。  
  
      你的 TableLayoutPanel 现在应该是一个 4x4 网格，包含十六个大小相等的方块单元格。 图标图像稍后会显示在这些行和列中。  
  
7. 确保在窗体编辑器中选择了该 TableLayoutPanel。 若要验证这一点，可查看“属性”窗口顶部的“tableLayoutPanel1”。 如果未选择，请在窗体上选择 TableLayoutPanel 或在“属性”窗口顶部的下拉控件中选择它。  
  
    选择 TableLayoutPanel 后，打开工具箱并向 TableLayoutPanel 的左上角单元格添加“Label”控件（位于“公共控件”类别中）。 现在，`Label` 控件在 IDE 中应处于选中状态。 为其设置下列属性。  
  
   1. 请确保将标签的“BackColor”属性设置为“CornflowerBlue”。  
  
   2. 将“AutoSize”属性设置为“False”。  
  
   3. 将“Dock”属性设置为“Fill”。  
  
   4. 通过选择“TextAlign”属性旁的下拉按钮并选择中间按钮，将该属性设置为“MiddleCenter”。 这将确保图标显示在单元格中间。  
  
   5. 选择“Font”属性。 此时应显示一个省略号 (...) 按钮。  
  
   6. 选择省略号按钮，并将“Font”值设置为“Webdings”，将“Font Style”设置为“Bold”，并将“Size”设置为“72”。  
  
   7. 将标签的“Text”属性设置为字母“c”。  
  
        TableLayoutPanel 中的左上角单元格现在应包含一个位于蓝色背景中心的黑色框。  
  
       > [!NOTE]
       > Webdings 字体是 Windows 操作系统附带的图标字体。 在匹配游戏中，玩家需要匹配图标对，因此您使用此字体显示要匹配的图标。 不要在“Text”属性中输入“c”，请尝试输入其他字母以查看显示哪些图标。 感叹号是一个蜘蛛，大写 N 是一只眼，逗号是一个红辣椒。  
  
8. 选择你的标签控件并将其复制到 TableLayoutPanel 中的下一单元格。 （按 Ctrl+C 键，或在菜单栏上依次选择“编辑”、“复制”。）然后粘贴。 （按 Ctrl+V 键，或在菜单栏上依次选择“编辑”、“粘贴”。）第一个标签的副本将显示在 TableLayoutPanel 的第二个单元格中。 再次粘贴它，在第三个单元格中会出现另一个标签。 一直粘贴 `Label` 控件，直到填充完所有单元格。  
  
   > [!NOTE]
   > 如果粘贴次数太多，IDE 会将一个新行添加到 TableLayoutPanel 中，以便提供添加新标签控件的位置。 您可以撤消此操作。 若要删除新单元格，请按 Ctrl+Z 键，或在菜单栏上依次选择“编辑”、“撤消”。  
  
    现在，窗体布局已设置完毕。其外观应类似于下图。  
  
    ![初始匹配游戏窗体](../ide/media/express-tut4step1.png "Express_Tut4Step1")  
   初始匹配游戏窗体  
  
### <a name="to-continue-or-review"></a>继续或查看  
  
- 要转到下一个教程步骤，请参阅[步骤 2：添加随机对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)。  
  
- 要返回概述主题，请参阅[教程 3：创建匹配游戏](../ide/tutorial-3-create-a-matching-game.md)。
