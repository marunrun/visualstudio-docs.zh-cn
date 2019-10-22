---
title: 在 Outlook 中用电子邮件显示自定义任务窗格
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], displaying with e-mail messages
- displaying custom task panes in e-mail
- e-mail [Office development in Visual Studio], custom task panes displayed in
- custom task panes [Office development in Visual Studio], displaying with e-mail messages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 40ff277ff5102c436a6815af3b542894c8061e56
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255595"
---
# <a name="walkthrough-display-custom-task-panes-with-email-messages-in-outlook"></a>演练：在 Outlook 中用电子邮件显示自定义任务窗格
  本演练演示如何使用创建或打开的每封电子邮件显示自定义任务窗格的唯一实例。 用户可以通过使用每封电子邮件功能区中的按钮显示或隐藏自定义任务窗格。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 若要使用多个资源管理器或检查器窗口显示自定义任务窗格，则必须为打开的每个窗口创建自定义任务窗格的实例。 有关 Outlook 窗口中自定义任务窗格的行为的详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

> [!NOTE]
> 本演练分小段展示 VSTO 外接程序代码以便更容易讨论代码背后的逻辑。

 本演练阐释了以下任务：

- 设计自定义任务窗格的用户界面 (UI)。

- 创建自定义功能区 UI。

- 用电子邮件显示自定义功能区 UI。

- 创建一个类来管理检查器窗口和自定义任务窗格。

- 初始化和清理 VSTO 外接程序使用的资源。

- 将功能区切换按钮与自定义任务窗格同步。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] 或 Microsoft Outlook 2010。

  ![视频链接](../vsto/media/playvideo.gif "视频链接")有关相关的视频演示，请[参阅如何实现：使用 Outlook 中的任务窗格？](http://go.microsoft.com/fwlink/?LinkID=130309).

## <a name="create-the-project"></a>创建项目
 在 VSTO 加载项中实现自定义任务窗格。首先为 Outlook 创建 VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 创建名为 **OutlookMailItemTaskPane** 的“Outlook 外接程序”项目。 使用“Outlook 外接程序” 项目模板。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 此时将打开 *ThisAddIn.cs* 或 *ThisAddIn.vb* 代码文件，并将“OutlookMailItemTaskPane” 项目添加到“解决方案资源管理器”。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>设计自定义任务窗格的用户界面
 自定义任务窗格没有可视化设计器，但你可以设计具有所需 UI 的用户控件。 此 VSTO 外接程序中的自定义任务窗格具有一个包含 <xref:System.Windows.Forms.TextBox> 控件的简单 UI。 稍后在本演练中，你将向自定义任务窗格添加用户控件。

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>若要设计自定义任务窗格的用户界面

1. 在“解决方案资源管理器”中，单击“OutlookMailItemTaskPane” 项目。

2. 在 **“项目”** 菜单上，单击 **“添加用户控件”** 。

3. 在“添加新项” 对话框中，将用户控件的名称更改为 **TaskPaneControl**，然后单击“添加”。

     用户控件将在设计器中打开。

4. 从“工具箱” 的“公共控件”选项卡中，将 **TextBox** 控件拖到用户控件中。

## <a name="design-the-user-interface-of-the-ribbon"></a>设计功能区的用户界面
 此 VSTO 外接程序的目标之一是为用户提供一种从每封电子邮件的功能区隐藏或显示自定义任务窗格的方法。 若要提供用户界面，请创建显示切换按钮的自定义功能区 UI，用户可以单击此按钮以显示或隐藏自定义任务窗格。

### <a name="to-create-a-custom-ribbon-ui"></a>若要创建自定义功能区 UI

1. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”** 。

3. 将新功能区更名为 **ManageTaskPaneRibbon**，然后单击“添加”。

     *ManageTaskPaneRibbon.cs* 或 *ManageTaskPaneRibbon.vb* 文件将在功能区设计器中打开，并显示一个默认选项卡和组。

4. 在功能区设计器中，单击“Group1”。

5. 在“属性” 窗口中，将“Label”属性 设置为 **Task Pane Manager**。

6. 从“工具箱” 的“Office 功能区控件”选项卡中，将 ToggleButton 控件拖到“Task Pane Manager” 组。

7. 单击“toggleButton1”。

8. 在“属性” 窗口中，将“Label”属性 设置为 **Show Task Pane**。

## <a name="display-the-custom-ribbon-user-interface-with-email-messages"></a>用电子邮件显示自定义功能区用户界面
 在本演练中创建的自定义任务窗格设计为仅与包含电子邮件的检查器窗口一起显示。 因此，可将属性设置为仅使用这些窗口显示自定义功能区 UI。

### <a name="to-display-the-custom-ribbon-ui-with-email-messages"></a>用电子邮件显示自定义功能区 UI

1. 在功能区设计器中，单击“ManageTaskPaneRibbon” 功能区。

2. 在“属性” 窗口中，单击“RibbonType”旁边的下拉列表，然后选择 **Microsoft.Outlook.Mail.Compose** 和 **Microsoft.Outlook.Mail.Read**。

## <a name="create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>创建一个类来管理检查器窗口和自定义任务窗格
 在某些情况下，VSTO 外接程序必须标识与特定电子邮件关联的自定义任务窗格。 这些情况包括以下几种：

- 当用户关闭电子邮件时。 在这种情况下，VSTO 外接程序必须删除相应的自定义任务窗格以确保 VSTO 外接程序使用的资源被正确清理。

- 当用户关闭自定义任务窗格。 在这种情况下，VSTO 外接程序必须更新电子邮件的功能区上切换按钮的状态。

- 用户单击功能区上的切换按钮时。 在这种情况下，VSTO 外接程序必须隐藏或显示相应的任务窗格。

  若要启用 VSTO 外接程序来跟踪哪个自定义任务窗格与每个打开的电子邮件相关联，请创建一个包装<xref:Microsoft.Office.Interop.Outlook.Inspector>和<xref:Microsoft.Office.Tools.CustomTaskPane>对象对的自定义类。 此类为每封电子邮件创建一个新的自定义任务窗格对象，并在关闭相应的电子邮件时删除自定义任务窗格。

### <a name="to-create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>创建一个类来管理检查器窗口和自定义任务窗格

1. 在“解决方案资源管理器”中，右键单击“ThisAddIn.cs” 或“ThisAddIn.vb” 文件，然后单击“查看代码”。

2. 将下面的语句添加到文件的顶部。

     [!code-csharp[Trin_OutlookMailItemTaskPane#2](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#2)]
     [!code-vb[Trin_OutlookMailItemTaskPane#2](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#2)]

3. 将以下代码添加到 *类外部的* ThisAddIn.cs *或* ThisAddIn.vb `ThisAddIn` 文件中（对于 Visual C#，将此代码添加入 `OutlookMailItemTaskPane` 命名空间）。 `InspectorWrapper` 类管理一对 <xref:Microsoft.Office.Interop.Outlook.Inspector> 和 <xref:Microsoft.Office.Tools.CustomTaskPane> 对象。 你将在以下步骤中完成此类的定义。

     [!code-csharp[Trin_OutlookMailItemTaskPane#3](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#3)]
     [!code-vb[Trin_OutlookMailItemTaskPane#3](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#3)]

4. 将以下构造函数添加在上一步添加的代码后。 此构造函数创建并初始化与传入的 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象相关联的新自定义任务窗格。 在 C# 中，构造函数还将事件处理程序附加到 <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> 对象的 <xref:Microsoft.Office.Interop.Outlook.Inspector> 事件和 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> 对象的 <xref:Microsoft.Office.Tools.CustomTaskPane> 事件。

     [!code-csharp[Trin_OutlookMailItemTaskPane#4](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#4)]
     [!code-vb[Trin_OutlookMailItemTaskPane#4](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#4)]

5. 将以下方法添加在上一步添加的代码后。 此方法是 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> 类中包含的 <xref:Microsoft.Office.Tools.CustomTaskPane> 对象的 `InspectorWrapper` 事件。 每当用户打开或关闭自定义任务窗格时，此代码将更新切换按钮的状态。

     [!code-csharp[Trin_OutlookMailItemTaskPane#5](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#5)]
     [!code-vb[Trin_OutlookMailItemTaskPane#5](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#5)]

6. 将以下方法添加在上一步添加的代码后。 此方法是包含当前电子邮件的<xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> <xref:Microsoft.Office.Interop.Outlook.Inspector>对象的事件的事件处理程序。 此事件处理程序在电子邮件关闭时释放资源。 事件处理程序还会从 `CustomTaskPanes` 集合删除当前的自定义任务窗格。 这有助于在打开下一封电子邮件时阻止自定义任务窗格的多个实例。

     [!code-csharp[Trin_OutlookMailItemTaskPane#6](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#6)]
     [!code-vb[Trin_OutlookMailItemTaskPane#6](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#6)]

7. 将以下代码添加在上一步添加的代码后。 稍后在本演练中，你将从自定义功能区 UI 中的一个方法调用此属性，以显示或隐藏自定义任务窗格。

     [!code-csharp[Trin_OutlookMailItemTaskPane#7](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#7)]
     [!code-vb[Trin_OutlookMailItemTaskPane#7](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#7)]

## <a name="initialize-and-clean-up-resources-used-by-the-add-in"></a>初始化和清理外接程序使用的资源
 添加代码到 `ThisAddIn` 类以便在加载 VSTO 外接程序对其进行初始化，并在卸载 VSTO 外接程序时清理其使用的资源。 通过设置<xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector>事件的事件处理程序并将所有现有的电子邮件传递给此事件处理程序来初始化 VSTO 外接程序。 VSTO 外接程序卸载时，分离事件处理程序并清理 VSTO 外接程序使用的对象。

### <a name="to-initialize-and-clean-up-resources-used-by-the-vsto-add-in"></a>若要初始化和清理 VSTO 外接程序使用的资源

1. 在 *ThisAddIn.cs* 或 *ThisAddIn.vb* 文件中，找到 `ThisAddIn` 类的定义。

2. 将以下声明添加到 `ThisAddIn` 类中：

   - `inspectorWrappersValue` 字段包含由 VSTO 外接程序管理的所有 <xref:Microsoft.Office.Interop.Outlook.Inspector> 和 `InspectorWrapper` 对象。

   - `inspectors` 字段保留对当前 Outlook 实例中检查器窗口的集合的引用。 此引用可防止垃圾回收器释放包含 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> 事件的事件处理程序的内存，这点将在下一步中声明。

     [!code-csharp[Trin_OutlookMailItemTaskPane#8](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#8)]
     [!code-vb[Trin_OutlookMailItemTaskPane#8](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#8)]

3. 将 `ThisAddIn_Startup` 方法替换为以下代码。 此代码将事件处理程序附加到 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> 事件，并且它将每个现有 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象传递到事件处理程序。 如果用户在 Outlook 已经运行后加载 VSTO 外接程序，VSTO 外接程序将使用此信息为所有已打开的电子邮件创建自定义任务窗格。

    [!code-csharp[Trin_OutlookMailItemTaskPane#9](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#9)]
    [!code-vb[Trin_OutlookMailItemTaskPane#9](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#9)]

4. 将 `ThisAddIn_ShutDown` 方法替换为以下代码。 此代码将分离 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> 事件处理程序，并清理 VSTO 外接程序使用的对象。

    [!code-csharp[Trin_OutlookMailItemTaskPane#10](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#10)]
    [!code-vb[Trin_OutlookMailItemTaskPane#10](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#10)]

5. 向 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> 类添加以下 `ThisAddIn` 事件处理程序。 如果新<xref:Microsoft.Office.Interop.Outlook.Inspector>的包含电子邮件，则该方法将创建新`InspectorWrapper`对象的实例来管理电子邮件和相应的任务窗格之间的关系。

    [!code-csharp[Trin_OutlookMailItemTaskPane#11](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#11)]
    [!code-vb[Trin_OutlookMailItemTaskPane#11](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#11)]

6. 向 `ThisAddIn` 类添加以下属性。 此属性将私有 `inspectorWrappersValue` 字段公开为 `ThisAddIn` 类外部的代码。

    [!code-csharp[Trin_OutlookMailItemTaskPane#12](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#12)]
    [!code-vb[Trin_OutlookMailItemTaskPane#12](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#12)]

## <a name="checkpoint"></a>检查点
 生成项目以确保它在编译时没有错误。

### <a name="to-build-your-project"></a>若要生成你的项目

1. 在“解决方案资源管理器”中，右键单击 **OutlookMailItemTaskPane** 项目，然后单击“生成”。 验证此项目是否在编译时未发生错误。

## <a name="synchronize-the-ribbon-toggle-button-with-the-custom-task-pane"></a>将功能区切换按钮与自定义任务窗格同步
 当任务窗格可见时，切换按钮将显示为按下状态，当任务窗格隐藏时，其显示为未按下状态。 若要将按钮状态与自定义任务窗格同步，请修改切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件处理程序。

### <a name="to-synchronize-the-custom-task-pane-with-the-toggle-button"></a>若要将自定义任务窗格与切换按钮同步

1. 在功能区设计器中，双击“显示任务窗格” 切换按钮。

     Visual Studio 会自动生成名为 `toggleButton1_Click`的事件处理程序，它将处理切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件。 Visual Studio 还将打开代码编辑器中的 *ManageTaskPaneRibbon.cs* 或 *ManageTaskPaneRibbon.vb* 文件。

2. 将以下语句添加到 *ManageTaskPaneRibbon.cs* 或 *ManageTaskPaneRibbon.vb* 文件的顶部。

     [!code-csharp[Trin_OutlookMailItemTaskPane#14](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs#14)]
     [!code-vb[Trin_OutlookMailItemTaskPane#14](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb#14)]

3. 将 `toggleButton1_Click` 事件处理程序替换为以下代码。 当用户单击切换按钮时，此方法将隐藏或显示与当前检查器窗口相关联的自定义任务窗格。

     [!code-csharp[Trin_OutlookMailItemTaskPane#15](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs#15)]
     [!code-vb[Trin_OutlookMailItemTaskPane#15](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb#15)]

## <a name="test-the-project"></a>测试项目
 当开始调试项目时，会打开 Outlook 并且加载 VSTO 外接程序。 VSTO 外接程序显示每个打开的电子邮件的自定义任务窗格的唯一实例。 创建多个新的电子邮件以测试代码。

### <a name="to-test-the-vsto-add-in"></a>若要测试 VSTO 外接程序

1. 按 F5。

2. 在 Outlook 中，单击 "**新建**" 创建新的电子邮件。

3. 在电子邮件的功能区上，单击 "**外接程序**" 选项卡，然后单击 "**显示任务窗格**" 按钮。

    使用电子邮件验证标题为 **"我的任务窗格**" 的任务窗格。

4. 在任务窗格中，在文本框中键入 **First task pane** 。

5. 关闭任务窗格。

    验证“显示任务窗格” 的状态是否更改，以便此按钮不再按下。

6. 再次单击“显示任务窗格” 按钮。

    验证任务窗格是否打开，并且文本框中是否仍然包含字符串 **First task pane**。

7. 在 Outlook 中，单击 "**新建**" 以创建另一封电子邮件。

8. 在电子邮件的功能区上，单击 "**外接程序**" 选项卡，然后单击 "**显示任务窗格**" 按钮。

    使用电子邮件验证标题为 "**我的任务窗格**" 的任务窗格，并且此任务窗格中的文本框为空。

9. 在任务窗格中，在文本框中键入 **Second task pane** 。

10. 将焦点更改为第一封电子邮件。

     验证与此电子邮件关联的任务窗格是否仍然在文本框中显示**第一个任务窗格**。

    此 VSTO 外接程序还可以处理更高级的方案，你可以尝试。 例如，你可以通过使用 "**下一项**" 和 "**上一项**" 按钮来测试查看电子邮件的行为。 你还可以在卸载 VSTO 外接程序时测试行为，打开多个电子邮件，然后重新加载 VSTO 外接程序。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何创建自定义任务窗格的详细信息：

- 在其他应用程序的 VSTO 外接程序中创建自定义任务窗格。 有关支持自定义任务窗格的应用程序的详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

- 通过使用自定义任务窗格自动化 Microsoft Office 应用程序。 有关详细信息，请参见[演练：从自定义任务窗格](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)中自动执行应用程序。

- 在 Excel 中创建一个可用于隐藏或显示自定义任务窗格的功能区按钮。 有关详细信息，请参见[演练：同步自定义任务窗格与功能区按钮](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)。

## <a name="see-also"></a>请参阅
- [自定义任务窗格](../vsto/custom-task-panes.md)
- [如何：向应用程序添加自定义任务窗格](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [演练：从自定义任务窗格自动化应用程序](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [演练：将自定义任务窗格与功能区按钮同步](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
