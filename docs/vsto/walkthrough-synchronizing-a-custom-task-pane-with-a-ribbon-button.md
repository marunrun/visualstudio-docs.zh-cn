---
title: 将自定义任务窗格与功能区按钮同步
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom task panes [Office development in Visual Studio], showing and hiding
- showing custom task panes
- Ribbon [Office development in Visual Studio], custom task panes
- toggle buttons [Office development in Visual Studio]
- custom task panes [Office development in Visual Studio], synchronizing with Ribbon button
- user interfaces [Office development in Visual Studio], custom task panes
- synchronization [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], showing and hiding
- custom task panes [Office development in Visual Studio], creating
- hiding custom task panes
- task panes [Office development in Visual Studio], creating
- task panes [Office development in Visual Studio], synchronizing with Ribbon button
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ad910f94c6b6a4345f6973e84e02c85d4fe1f0e4
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328339"
---
# <a name="walkthrough-synchronize-a-custom-task-pane-with-a-ribbon-button"></a>演练：将自定义任务窗格与功能区按钮同步
  本演练演示如何创建用户可以隐藏或通过单击功能区上的切换按钮显示的自定义任务窗格。 应始终创建一个可供用户单击以显示或隐藏你的自定义任务窗格的用户界面 (UI) 元素，如按钮，因为 Microsoft Office 应用程序不提供用户用于显示或隐藏自定义任务窗格的默认方式。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 虽然本演练具体使用的是 Excel，但其中所阐释的概念同样适用于上面所列的应用程序。

 本演练阐释了以下任务：

- 设计自定义任务窗格的 UI。

- 向功能区添加切换按钮。

- 使用自定义任务窗格同步切换按钮。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel 或 Microsoft [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)]。

## <a name="create-the-add-in-project"></a>创建外接程序项目
 在此步骤中，将为 Excel 创建的 VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用 Excel 外接程序项目模板，创建一个名为 **SynchronizeTaskPaneAndRibbon**的 Excel 外接程序项目。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 打开 **ThisAddIn.cs** 或 **ThisAddIn.vb** 代码文件，并将 **SynchronizeTaskPaneAndRibbon** 项目添加到 **“解决方案资源管理器”** 。

## <a name="add-a-toggle-button-to-the-ribbon"></a>向功能区添加切换按钮
 Office 应用程序的设计准则之一是：用户应始终能控制 Office 应用程序 UI。 若要让用户可以控制自定义任务窗格，可以添加一个可显示和隐藏任务窗格的功能区切换按钮。 若要创建一个切换按钮，则将 **“功能区(可视化设计器)”** 项添加到项目。 设计器可帮助你添加和放置控件、设置控件属性以及处理控件事件。 有关详细信息，请参阅[功能区设计器](../vsto/ribbon-designer.md)。

### <a name="to-add-a-toggle-button-to-the-ribbon"></a>若要添加到功能区切换按钮

1. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”** 。

3. 将新功能区更名为 **ManageTaskPaneRibbon**，然后单击“添加”  。

     **ManageTaskPaneRibbon.cs** 或 **ManageTaskPaneRibbon.vb** 文件将在功能区设计器中打开，并显示一个默认选项卡和组。

4. 在功能区设计器中，单击“Group1”  。

5. 在“属性”  窗口中，将“Label”属性  设置为 **Task Pane Manager**。

6. 从“工具箱”  的“Office 功能区控件”  选项卡中，将 **ToggleButton** 拖到“Task Pane Manager”  组。

7. 单击“toggleButton1”  。

8. 在“属性”  窗口中，将“Label”属性  设置为 **Show Task Pane**。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>设计自定义任务窗格的用户界面
 没有针对自定义任务窗格的可视化设计器，但可以设计具有所需布局的用户控件。 稍后在本演练中，你将向自定义任务窗格添加用户控件。

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>若要设计自定义任务窗格的用户界面

1. 在 **“项目”** 菜单上，单击 **“添加用户控件”** 。

2. 在“添加新项”  对话框中，将用户控件的名称更改为 **TaskPaneControl**，然后单击“添加”  。

     用户控件将在设计器中打开。

3. 从“工具箱”  的“公共控件”  选项卡中，将 **TextBox** 控件拖到用户控件中。

## <a name="create-the-custom-task-pane"></a>创建自定义任务窗格
 若要在 VSTO 外接程序启动时创建自定义任务窗格，请将用户控件添加到 VSTO 外接程序的 <xref:Microsoft.Office.Tools.AddIn.Startup> 事件处理程序中的任务窗格中。 默认情况下，自定义任务窗格将不可见。 稍后在本演练中，您将添加代码，将显示或隐藏任务窗格中，当用户单击切换按钮添加到功能区。

### <a name="to-create-the-custom-task-pane"></a>若要创建自定义任务窗格

1. 在 **“解决方案资源管理器”** 中，展开 **“Excel”** 。

2. 右键单击 **ThisAddIn.cs** 或 **ThisAddIn.vb** ，然后单击“查看代码”  。

3. 向 `ThisAddIn` 类添加下面的代码。 此代码将 `TaskPaneControl` 的实例声明为 `ThisAddIn`的成员。

     [!code-csharp[Trin_TaskPaneRibbonSynchronize#1](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#1)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#1)]

4. 将 `ThisAddIn_Startup` 事件处理程序替换为以下代码。 此代码向 `TaskPaneControl` 字段添加 `CustomTaskPanes` 对象，但它不显示自定义任务窗格（默认情况下， <xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> 类的 <xref:Microsoft.Office.Tools.CustomTaskPane> 属性是 **false**）。 Visual C# 代码还会将一个事件处理程序附加到 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> 事件。

     [!code-csharp[Trin_TaskPaneRibbonSynchronize#2](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#2)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#2)]

5. 将以下方法添加到 `ThisAddIn` 类。 此方法处理 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> 事件。 当用户通过单击 **“关闭”** 按钮 (X) 来关闭任务窗格时，此方法将更新功能区上切换按钮的状态。

     [!code-csharp[Trin_TaskPaneRibbonSynchronize#3](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#3)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#3](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#3)]

6. 向 `ThisAddIn` 类添加以下属性。 此属性对其他类公开私有 `myCustomTaskPane1` 对象。 稍后在本演练中，你将向使用此属性的 `MyRibbon` 类添加代码。

     [!code-csharp[Trin_TaskPaneRibbonSynchronize#4](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#4)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#4](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#4)]

## <a name="hide-and-show-the-custom-task-pane-by-using-the-toggle-button"></a>隐藏和显示通过使用切换按钮的自定义任务窗格
 最后一步是添加可在用户单击功能区上的切换按钮时显示或隐藏自定义任务窗格的代码。

### <a name="to-display-and-hide-the-custom-task-pane-by-using-the-toggle-button"></a>通过使用切换按钮显示和隐藏自定义任务窗格

1. 在功能区设计器中，双击“显示任务窗格”  切换按钮。

     Visual Studio 会自动生成名为 `toggleButton1_Click`的事件处理程序，它将处理切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件。 Visual Studio 还会打开代码编辑器中的 *MyRibbon.cs* 或 *MyRibbon.vb* 文件。

2. 将 `toggleButton1_Click` 事件处理程序替换为以下代码。 当用户单击切换按钮时，此代码显示或隐藏自定义任务窗格，具体取决于是按下还是未按下切换按钮。

     [!code-vb[Trin_TaskPaneRibbonSynchronize#5](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.vb#5)]
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#5](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.cs#5)]

## <a name="test-the-add-in"></a>测试的外接程序
 运行项目时，Excel 会打开，但不显示自定义任务窗格。 单击要测试的代码的功能区上的切换按钮。

### <a name="to-test-your-vsto-add-in"></a>测试 VSTO 外接程序

1. 按**F5**运行你的项目。

     确认 Excel 打开，并**外接程序**选项卡显示在功能区。

2. 单击**外接程序**功能区上的选项卡。

3. 在 **“任务窗格管理器”** 组中，单击 **“显示任务窗格”** 切换按钮。

     验证当点击切换按钮时，任务窗格交替显示和隐藏。

4. 当任务窗格可见时，单击任务窗格一角的 **“关闭”** 按钮 (X)。

     验证切换按钮显示为未按下。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何创建自定义任务窗格的详细信息：

- 在 VSTO 外接程序中的其他应用程序中创建自定义任务窗格。 有关支持自定义任务窗格的应用程序的详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

- 从自定义任务窗格自动化应用程序。 有关详细信息，请参见[演练：自动执行应用程序从自定义任务窗格](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)。

- 为 Outlook 中打开的每封电子邮件创建自定义任务窗格。 有关详细信息，请参见[演练：在 Outlook 中显示的电子邮件消息的自定义任务窗格](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)。

## <a name="see-also"></a>请参阅
- [自定义任务窗格](../vsto/custom-task-panes.md)
- [如何：向应用程序添加自定义任务窗格](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [演练：自动执行从自定义任务窗格应用程序](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [演练：在 Outlook 中显示电子邮件消息的自定义任务的窗格](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
- [功能区概述](../vsto/ribbon-overview.md)
