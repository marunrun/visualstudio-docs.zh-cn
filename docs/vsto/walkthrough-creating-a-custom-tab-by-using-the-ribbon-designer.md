---
title: 演练：使用功能区设计器创建自定义选项卡
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], controlling from Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon Designer [Office development in Visual Studio]
- customizing the Ribbon, tabs
- custom Ribbon, tabs
- Custom tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3a56f8bdfed38d77a939ab8e8b159510da7fcb15
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438608"
---
# <a name="walkthrough-create-a-custom-tab-by-using-the-ribbon-designer"></a>演练：使用功能区设计器创建自定义选项卡
  使用功能区设计器，可以创建自定义选项卡，然后在其中添加和放置控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- [创建操作窗格](#BKMK_CreateActionsPanes)。

- [创建自定义选项卡](#BKMK_CreateCustomTab)。

- [隐藏和显示操作窗格使用自定义选项卡上的按钮](#BKMK_HideShowActionsPane)。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-an-excel-workbook-project"></a>创建的 Excel 工作簿项目
 使用功能区设计器的步骤对于所有 Office 应用程序几乎是相同的。 本示例使用一个 Excel 工作簿。

### <a name="to-create-an-excel-workbook-project"></a>创建 Excel 工作簿项目

- 使用名称创建的 Excel 工作簿项目**为 myexcelribbon**。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新的工作簿并将添加**为 myexcelribbon**投影到**解决方案资源管理器**。

## <a name="BKMK_CreateActionsPanes"></a> 创建操作窗格
 将两个自定义操作窗格添加到项目。 稍后会将显示和隐藏这些操作窗格的按钮添加到自定义选项卡中。

### <a name="to-create-actions-panes"></a>创建操作窗格

1. 在 **“项目”** 菜单上选择 **“添加新项”**。

2. 在中**添加新项**对话框中，选择**ActionsPaneControl**，然后选择**添加**。

     **ActionsPaneControl1.cs**或**ActionsPaneControl1.vb**文件将在设计器中打开。

3. 从**公共控件**选项卡**工具箱**，向设计器图面添加一个标签。

4. 在中**属性**窗口中，将**文本**属性到 label1**操作窗格 1**。

5. 重复步骤 1 至 5，再创建一个操作窗格和标签。 设置**文本**到第二个标签的属性**操作窗格 2**。

## <a name="BKMK_CreateCustomTab"></a> 创建自定义选项卡
 Office 应用程序的设计准则之一是：用户应始终能控制 Office 应用程序 UI。 若要为操作窗格添加此功能，可以添加用于从功能区上的自定义选项卡显示和隐藏每个操作窗格的按钮。 若要创建自定义选项卡，添加**功能区 （可视化设计器）** 到项目的项。 设计器可帮助你添加和放置控件、设置控件属性以及处理控件事件。

### <a name="to-create-a-custom-tab"></a>创建自定义选项卡

1. 在 **“项目”** 菜单上选择 **“添加新项”**。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”**。

3. 更改到新的功能区的名称**MyRibbon**，然后选择**添加**。

     **MyRibbon.cs** 或 **MyRibbon.vb** 文件将在功能区设计器中打开，并显示一个默认选项卡和组。

4. 在功能区设计器中，选择默认选项卡。

5. 在中**属性**窗口中，展开**ControlId**属性，且然后将设置**ControlIdType**属性设置为**自定义**。

6. 设置**标签**属性设置为**我的自定义选项卡**。

7. 在功能区设计器中，选择**group1**。

8. 在中**属性**窗口中，将**标签**到**操作窗格管理器**。

9. 从**Office 功能区控件**选项卡**工具箱**，将按钮拖动到**group1**。

10. 选择**button1**。

11. 在中**属性**窗口中，将**标签**到**显示操作窗格 1**。

12. 添加到第二个按钮**group1**，并设置**标签**属性设置为**显示操作窗格 2**。

13. 从**Office 功能区控件**选项卡**工具箱**，将**ToggleButton**控件拖动到**group1**。

14. 设置**标签**属性设置为**隐藏操作窗格**。

## <a name="BKMK_HideShowActionsPane"></a> 隐藏和显示操作窗格使用自定义选项卡上的按钮
 最后一个步骤是添加对用户进行响应的代码。 为上述两个按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> 事件和切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件添加事件处理程序。 在这些事件处理程序中添加相应代码即可隐藏和显示操作窗格。

### <a name="to-hide-and-show-actions-panes-by-using-buttons-in-the-custom-tab"></a>使用自定义选项卡中的按钮隐藏和显示操作窗格

1. 在中**解决方案资源管理器**，打开快捷菜单*MyRibbon.cs*或*MyRibbon.vb*，然后选择**查看代码**。

2. 将下面的代码添加到 `MyRibbon` 类的顶部。 这段代码可以创建两个操作窗格对象。

     [!code-csharp[Trin_Ribbon_Custom_Tab#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb#1)]

3. 将 `MyRibbon_Load` 方法替换为以下代码。 这段代码会将操作窗格对象添加到 <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> 集合中，并在视图中这些隐藏对象。 Visual C# 代码还会将委托附加到多个功能区控件事件。

     [!code-csharp[Trin_Ribbon_Custom_Tab#2](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs#2)]
     [!code-vb[Trin_Ribbon_Custom_Tab#2](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb#2)]

4. 将以下三个事件处理程序方法添加到 `MyRibbon` 类。 这些方法处理上述两个按钮 <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> 事件和切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件。 button1 和 button2 的事件处理程序显示两个交替出现的操作窗格。 toggleButton1 的事件处理程序显示和隐藏活动操作窗格。

     [!code-csharp[Trin_Ribbon_Custom_Tab#3](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs#3)]
     [!code-vb[Trin_Ribbon_Custom_Tab#3](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb#3)]

## <a name="test-the-custom-tab"></a>测试自定义选项卡
 运行项目，会启动 Excel 时，**我的自定义选项卡**选项卡显示在功能区。 在选择按钮**我的自定义选项卡**以显示和隐藏操作窗格。

### <a name="to-test-the-custom-tab"></a>测试自定义选项卡

1. 按**F5**运行你的项目。

2. 选择**我的自定义选项卡**选项卡。

3. 在中**自定义操作窗格管理器**组中，选择**显示操作窗格 1**。

     操作窗格将显示，并显示标签**操作窗格 1**。

4. 选择**显示操作窗格 2**。

     操作窗格将显示，并显示标签**操作窗格 2**。

5. 选择**隐藏操作窗格**。

     操作窗格不再可见。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Office 用户界面的更多信息：

- 将基于上下文的 UI 添加到任何文档级自定义项。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

- 扩展标准的或自定义的 Microsoft Office Outlook 窗体。 有关详细信息，请参见[演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)。

## <a name="see-also"></a>请参阅
- [在运行时在功能区的访问](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [为 Outlook 中自定义功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：将控件添加到 backstage 视图](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)
