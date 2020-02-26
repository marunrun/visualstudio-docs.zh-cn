---
title: 步骤 1：创建项目并向窗体添加表
ms.date: 10/15/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.assetid: 1cac4ba4-f3cd-43bd-ad5d-50fc599234e8
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c1134fb5bb02bd8c78f347ef582f12da35074c36
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579924"
---
# <a name="step-1-create-a-project-and-add-a-table-to-your-form"></a>步骤 1：创建项目并向窗体添加表

创建匹配游戏的第一步是创建项目并向窗体添加表。 该表有助于将图标对齐到有序的 4x4 网格。 你还要设置若干属性，以改善游戏板的外观。

## <a name="to-create-a-project-and-add-a-table-to-your-form"></a>创建项目并向窗体添加表

::: moniker range="vs-2017"

1. 在菜单栏上，依次选择“文件”  >“新建”  >“项目”  。

1. 在“新建项目”  对话框的左侧，选择 Visual C#  或 Visual Basic  ，然后选择“Windows 桌面”  。

1. 在模板列表中，选择“Windows 窗体应用(.NET Framework)”  模板，将其命名为“MatchingGame”  ，然后选择“确定”  按钮。

    此时将显示名为“Form1.cs”或“Form1.vb”的窗体，具体取决于所选择的编程语言。  

   > [!NOTE]
   > 如果没有看到“Windows 窗体应用(.NET Framework)”模板，请使用 Visual Studio 安装程序安装“.NET 桌面开发”工作负载   。<br/><br/>![Visual Studio 安装程序中的 .NET 桌面开发工作负载](../ide/media/dot-net-desktop-dev-workload.png)<br/><br/> 有关详细信息，请参阅[安装 Visual Studio](../install/install-visual-studio.md) 页面。

::: moniker-end

::: moniker range="vs-2019"

1. 在“开始”窗口上，选择“创建新项目”  。

   ![查看“创建新项目”窗口](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”  窗口的搜索框中输入或键入“Windows 窗体”  。 接下来，从“项目类型”列表中选择“桌面”   。

   应用“项目类型”筛选器之后，为 C# 或 Visual Basic 选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步”    。

   ![为“Windows 窗体应用 (.NET Framework)”选择 C# 或 Visual Basic 模板](./media/create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”  模板，则可以通过“创建新项目”  窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”  工作负载。
   >
   > ![Visual Studio 安装程序中的 .NET Core 开发工作负载](../ide/media/install-dot-net-desktop-env.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。

1. 在“配置新项目”  窗口中，在“项目名称”  框中键入或输入“MatchingGame”  。 然后，选择“创建”  。

::: moniker-end

## <a name="to-set-properties-for-a-form"></a>设置窗体属性

1. 在“属性”窗口中，设置下列窗体属性  。

   1. 将窗体的“Text”属性从“Form1”更改为“Matching Game”    。 该文本显示在游戏窗口的顶部。

   2. 将窗体大小设置为 550 像素（宽）× 550 像素（高）。 设置方法有两种：将“Size”属性设置为“550, 550”；或者拖拽窗体的边角，直至你在集成开发环境 (IDE) 的右下角看到正确大小   。

2. 通过选择 IDE 左侧的“工具箱”选项卡显示工具箱  。

3. 从工具箱中的“容器”类别拖动一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件，然后为其设置以下属性  。

   1. 将“BackColor”属性设置为“CornflowerBlue”   。 为此，请通过选择“属性”窗口中“BackColor”属性旁边的下拉箭头，打开“BackColor”对话框    。  然后，选择“BackColor”对话框中的“Web”选项卡，查看可用颜色名称的列表   。

      > [!NOTE]
      > 这些颜色未按字母顺序排列，CornflowerBlue  位于列表底部附近。

   2. 通过选择“Dock”属性旁边的下拉按钮并选择大的中间按钮，将该属性设置为“Fill”   。 这会扩展该表，使其覆盖整个窗体。

   3. 将“CellBorderStyle”属性设置为“Inset”   。 这会在游戏板上每个单元格之间提供可视边框。

   4. 选择 TableLayoutPanel 右上角的三角形按钮，以显示任务菜单。

   5. 在任务菜单上，选择“添加行”两次以再添加两行，然后选择“添加列”两次以再添加两列   。

   6. 在任务菜单上，选择“编辑行和列”，打开“列和行样式”窗口   。 选择每一列，再选择“百分比”选项按钮，然后将每列的宽度设置为总宽度的 25%  。 然后从窗口顶部的下拉框选择“行”，并将每个行的高度设置为 25%  。 完成后，选择“确定”按钮  。

      你的 TableLayoutPanel 现在应该是一个 4x4 网格，包含十六个大小相等的方块单元格。 图标图像稍后会显示在这些行和列中。

4. 确保在窗体编辑器中选择了该 TableLayoutPanel。 若要验证这一点，可查看“属性”窗口顶部的“tableLayoutPanel1”   。 如果未选择，请在窗体上选择 TableLayoutPanel 或在“属性”窗口顶部的下拉控件中选择它  。

    选择“TableLayoutPanel”后，打开“工具箱”并向 TableLayoutPanel 的左上角单元格添加 <xref:System.Windows.Forms.Label> 控件（位于“公共控件”  类别中）。 现在，Label 控件在 IDE 中应处于选中状态。 为其设置下列属性。

   1. 请确保将标签的“BackColor”属性设置为“CornflowerBlue”   。

   2. 将“AutoSize”属性设置为“False”。  

   3. 将“Dock”属性设置为“Fill”   。

   4. 通过选择“TextAlign”属性旁的下拉按钮并选择中间按钮，将该属性设置为“MiddleCenter”   。 这将确保图标显示在单元格中间。

   5. 选择“Font”属性  。 此时应显示一个省略号 (...  ) 按钮。

   6. 选择省略号按钮，并将“Font”值设置为“Webdings”，将“Font Style”设置为“Bold”，并将“Size”设置为“48”       。

   7. 将标签的“Text”属性设置为字母“c”   。

        TableLayoutPanel 中的左上角单元格现在应包含一个位于蓝色背景中心的黑色框。

       > [!NOTE]
       > Webdings 字体是 Windows 操作系统附带的图标字体。 在匹配游戏中，玩家需要匹配图标对，因此您使用此字体显示要匹配的图标。 不要在“Text”属性中输入“c”，请尝试输入其他字母以查看显示哪些图标   。 感叹号是一个蜘蛛，大写 N 是一只眼，逗号是一个红辣椒。

5. 选择你的 Label 控件并将其复制到 TableLayoutPanel 中的下一单元格。 （按 Ctrl  +C  键，或在菜单栏上依次选择“编辑”   > “复制”  。）然后粘贴。 （按 Ctrl  +V  键，或在菜单栏上依次选择“编辑”   > “粘贴”  。）第一个 Label 的副本将显示在 TableLayoutPanel 的第二个单元格中。 再次粘贴它，在第三个单元格中会出现另一 Label。 一直粘贴 Label 控件，直到填充完所有单元格。

   > [!NOTE]
   > 如果粘贴次数太多，IDE 会将一个新行添加到 TableLayoutPanel 中，以便提供添加新 Label 控件的位置。 您可以撤消此操作。 若要删除新单元格，请按 Ctrl  +Z  键，或在菜单栏上依次选择“编辑”   > “撤消”  。

    现在，窗体布局已设置完毕。它应如下图所示。

    ![初始匹配游戏窗体](../ide/media/express_tut4step1.png)<br/>*初始匹配游戏窗体*

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 2：添加 Random 对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)中添加的列表拉取随机图标。

- 要返回概述主题，请参阅[教程 3：创建匹配游戏](../ide/tutorial-3-create-a-matching-game.md)。
