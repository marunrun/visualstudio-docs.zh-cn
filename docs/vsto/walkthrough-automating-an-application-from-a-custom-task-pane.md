---
title: 演练：从自定义任务窗格自动化应用程序
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio], custom task panes
- automating Office applications
- custom task panes [Office development in Visual Studio], automating applications
- custom task panes [Office development in Visual Studio], PowerPoint
- task panes [Office development in Visual Studio], automating applications
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f5135e96125192d7ed125287aa47c839031824fe
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871940"
---
# <a name="walkthrough-automate-an-application-from-a-custom-task-pane"></a>演练：从自定义任务窗格自动化应用程序
  本演练演示了如何创建实现 PowerPoint 自动化的自定义任务窗格。 当用户单击自定义任务窗格中的 <xref:System.Windows.Forms.MonthCalendar> 控件时，自定义任务窗格向一张幻灯片中插入日期。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 虽然本演练具体使用的是 PowerPoint，但其中所阐释的概念同样适用于上面所列的应用程序。

 本演练阐释了以下任务：

- 设计自定义任务窗格的用户界面。

- 从自定义任务窗格中实现 PowerPoint 自动化。

- 在 PowerPoint 中显示自定义任务窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft PowerPoint 2010 或 [!INCLUDE[PowerPoint_15_short](../vsto/includes/powerpoint-15-short-md.md)]。

## <a name="create-the-add-in-project"></a>创建外接程序项目
 第一步是创建 PowerPoint 的 VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用 PowerPoint 外接程序项目模板创建名为 **MyAddIn**的 PowerPoint VSTO 外接程序项目。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将打开 **ThisAddIn.cs** 或 **ThisAddIn.vb** 代码文件并将 **MyAddIn** 项目添加到 **解决方案资源管理器**中。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>设计自定义任务窗格的用户界面
 没有针对自定义任务窗格的可视化设计器，但可以设计具有所需布局的用户控件。 稍后在本演练中，你将向自定义任务窗格添加用户控件。

#### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>若要设计自定义任务窗格的用户界面

1. 在 **“项目”** 菜单上，单击 **“添加用户控件”** 。

2. 在“添加新项” 对话框中，将用户控件的名称更改为 **MyUserControl**，然后单击“添加”。

     用户控件将在设计器中打开。

3. 从“工具箱” 的“公共控件”选项卡中，将 **MonthCalendar** 控件拖到用户控件中。

     如果 **MonthCalendar** 控件大于用户控件的设计图面，则调整用户控件的大小以适合 **MonthCalendar** 控件。

## <a name="automate-powerpoint-from-the-custom-task-pane"></a>从自定义任务窗格中实现 PowerPoint 自动化
 VSTO 外接程序的作用是在活动演示文稿的第一张幻灯片中放置所选日期。 使用控件的 <xref:System.Windows.Forms.MonthCalendar.DateChanged> 事件以在发生更改时添加所选日期。

### <a name="to-automate-powerpoint-from-the-custom-task-pane"></a>若要从自定义任务窗格中实现 PowerPoint 自动化

1. 在设计器中，双击 <xref:System.Windows.Forms.MonthCalendar> 控件。

     此时会打开 **MyUserControl.cs** 或 **MyUserControl.vb** 文件，并创建 <xref:System.Windows.Forms.MonthCalendar.DateChanged> 事件的事件处理程序。

2. 将下面的代码添加到文件的顶部。 此代码为<xref:Microsoft.Office.Core>和[PowerPoint](/previous-versions/office/developer/office-2010/ff763170%28v%3doffice.14%29)命名空间创建别名。

     [!code-csharp[Trin_TaskPaneMonthCalendar#1](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#1)]
     [!code-vb[Trin_TaskPaneMonthCalendar#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#1)]

3. 向 `MyUserControl` 类添加下面的代码。 此代码将[形状](/previous-versions/office/developer/office-2010/ff760244(v=office.14))对象声明为的成员`MyUserControl`。 在下面的步骤中, 您将使用此[形状](/previous-versions/office/developer/office-2010/ff760244(v=office.14))向活动演示文稿的幻灯片中添加文本框。

     [!code-csharp[Trin_TaskPaneMonthCalendar#2](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#2)]
     [!code-vb[Trin_TaskPaneMonthCalendar#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#2)]

4. 将 `monthCalendar1_DateChanged` 事件处理程序替换为以下代码。 此代码向活动演示文稿的第一张幻灯片中添加文本框，然后向文本框中添加当前选定的日期。 此代码将使用 `Globals.ThisAddIn` 对象来访问 PowerPoint 的对象模型。

     [!code-csharp[Trin_TaskPaneMonthCalendar#3](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#3)]
     [!code-vb[Trin_TaskPaneMonthCalendar#3](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#3)]

5. 在 **解决方案资源管理器**中，右键单击 **MyAddIn** 项目，然后单击“生成”。 验证此项目是否已生成且未发生错误。

## <a name="display-the-custom-task-pane"></a>显示自定义任务窗格
 若要在 VSTO 外接程序启动时显示自定义任务窗格，请将用户控件添加到 VSTO 外接程序的 <xref:Microsoft.Office.Tools.AddIn.Startup> 事件处理程序中的任务窗格中。

### <a name="to-display-the-custom-task-pane"></a>若要显示自定义任务窗格

1. 在 **解决方案资源管理器**中，展开 **PowerPoint**。

2. 右键单击 **ThisAddIn.cs** 或 **ThisAddIn.vb** ，然后单击“查看代码”。

3. 向 `ThisAddIn` 类添加下面的代码。 此代码将 `MyUserControl` 和 <xref:Microsoft.Office.Tools.CustomTaskPane> 的实例声明为 `ThisAddIn` 类的成员。

     [!code-vb[Trin_TaskPaneMonthCalendar#4](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb#4)]
     [!code-csharp[Trin_TaskPaneMonthCalendar#4](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs#4)]

4. 将 `ThisAddIn_Startup` 事件处理程序替换为以下代码。 此代码通过将 <xref:Microsoft.Office.Tools.CustomTaskPane> 对象添加到 `MyUserControl` 集合来创建新 `CustomTaskPanes` 。 代码还将显示任务窗格。

     [!code-vb[Trin_TaskPaneMonthCalendar#5](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb#5)]
     [!code-csharp[Trin_TaskPaneMonthCalendar#5](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs#5)]

## <a name="test-the-add-in"></a>测试外接程序
 运行该项目时，会打开 PowerPoint，VSTO 外接程序将显示自定义任务窗格。 单击 <xref:System.Windows.Forms.MonthCalendar> 控件以测试代码。

### <a name="to-test-your-vsto-add-in"></a>测试 VSTO 外接程序

1. 按**F5**运行项目。

2. 确认自定义任务窗格是可见的。

3. 单击任务窗格上 <xref:System.Windows.Forms.MonthCalendar> 控件中的某个日期。

     将向活动演示文稿的第一张幻灯片中添加日期。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何创建自定义任务窗格的详细信息：

- 在其他应用程序的 VSTO 外接程序中创建自定义任务窗格。 有关支持自定义任务窗格的应用程序的详细信息, 请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

- 创建一个用于隐藏或显示自定义任务窗格的功能区按钮。 有关详细信息，请参见[演练：同步自定义任务窗格与功能区按钮](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)。

- 为 Outlook 中打开的每封电子邮件创建自定义任务窗格。 有关详细信息，请参见[演练：在 Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)中用电子邮件显示自定义任务窗格。

## <a name="see-also"></a>请参阅
- [自定义任务窗格](../vsto/custom-task-panes.md)
- [如何：向应用程序添加自定义任务窗格](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [演练：将自定义任务窗格与功能区按钮同步](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [演练：在 Outlook 中用电子邮件显示自定义任务窗格](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
