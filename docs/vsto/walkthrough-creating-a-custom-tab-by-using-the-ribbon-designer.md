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
ms.openlocfilehash: 5a32cfc84aa9bc93761dc8b57c13651eb04031a2
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255528"
---
# <a name="walkthrough-create-a-custom-tab-by-using-the-ribbon-designer"></a>演练：使用功能区设计器创建自定义选项卡
  使用功能区设计器，可以创建自定义选项卡，然后在其中添加和放置控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- [创建操作窗格](#BKMK_CreateActionsPanes)。

- [创建自定义选项卡](#BKMK_CreateCustomTab)。

- [使用 "自定义" 选项卡上的按钮隐藏和显示操作窗格](#BKMK_HideShowActionsPane)。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-an-excel-workbook-project"></a>创建 Excel 工作簿项目
 使用功能区设计器的步骤对于所有 Office 应用程序几乎是相同的。 本示例使用一个 Excel 工作簿。

### <a name="to-create-an-excel-workbook-project"></a>创建 Excel 工作簿项目

- 创建名为**MyExcelRibbon**的 Excel 工作簿项目。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

     Visual Studio 将在设计器中打开新的工作簿，并将**MyExcelRibbon**项目添加到**解决方案资源管理器**。

## <a name="BKMK_CreateActionsPanes"></a>创建操作窗格
 将两个自定义操作窗格添加到项目。 稍后会将显示和隐藏这些操作窗格的按钮添加到自定义选项卡中。

### <a name="to-create-actions-panes"></a>创建操作窗格

1. 在 **“项目”** 菜单上选择 **“添加新项”** 。

2. 在 "**添加新项**" 对话框中，选择 " **ActionsPaneControl**"，然后选择 "**添加**"。

     **ActionsPaneControl1.cs**或**actionspanecontrol1.vb**文件将在设计器中打开。

3. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将一个标签添加到设计器图面。

4. 在 "**属性**" 窗口中，将 label1 的 " **Text** " 属性设置为 "**操作窗格 1**"。

5. 重复步骤 1 至 5，再创建一个操作窗格和标签。 将第二个标签的 " **Text** " 属性设置为 "**操作窗格 2**"。

## <a name="BKMK_CreateCustomTab"></a>创建自定义选项卡
 Office 应用程序的设计准则之一是：用户应始终能控制 Office 应用程序 UI。 若要为操作窗格添加此功能，可以添加用于从功能区上的自定义选项卡显示和隐藏每个操作窗格的按钮。 若要创建自定义选项卡，请将 "**功能区（可视化设计器）** " 项添加到项目。 设计器可帮助你添加和放置控件、设置控件属性以及处理控件事件。

### <a name="to-create-a-custom-tab"></a>创建自定义选项卡

1. 在 **“项目”** 菜单上选择 **“添加新项”** 。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”** 。

3. 将新功能区的名称更改为**myribbon.vb**，然后选择 "**添加**"。

     **MyRibbon.cs** 或 **MyRibbon.vb** 文件将在功能区设计器中打开，并显示一个默认选项卡和组。

4. 在功能区设计器中，选择默认选项卡。

5. 在 "**属性**" 窗口中，展开 " **ControlId** " 属性，然后将 " **ControlIdType** " 属性设置为 "**自定义**"。

6. 将 "**标签**" 属性设置为 **"自定义" 选项卡**。

7. 在功能区设计器中，选择 " **group1**"。

8. 在 "**属性**" 窗口中，将 "**标签**" 设置为 "**操作窗格管理器**"。

9. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将一个按钮拖到 " **group1**"。

10. 选择 " **button1**"。

11. 在 "**属性**" 窗口中，将 "**标签**" 设置为 "**显示操作窗格 1**"。

12. 将第二个按钮添加到 " **group1**"，并将 "**标签**" 属性设置为 "**显示操作窗格 2**"。

13. 从 "**工具箱**" 的 " **Office 功能区控件**" 选项卡中，将**切换按钮**控件拖到 " **group1**"。

14. 将 "**标签**" 属性设置为 "**隐藏操作窗格**"。

## <a name="BKMK_HideShowActionsPane"></a>使用 "自定义" 选项卡上的按钮隐藏和显示操作窗格
 最后一个步骤是添加对用户进行响应的代码。 为上述两个按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> 事件和切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件添加事件处理程序。 在这些事件处理程序中添加相应代码即可隐藏和显示操作窗格。

### <a name="to-hide-and-show-actions-panes-by-using-buttons-in-the-custom-tab"></a>使用自定义选项卡中的按钮隐藏和显示操作窗格

1. 在**解决方案资源管理器**中，打开*MyRibbon.cs*或*myribbon.vb*的快捷菜单，然后选择 "**查看代码**"。

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
 运行该项目时，Excel 将开始，"**我的自定义选项**卡" 选项卡将显示在功能区上。 选择 "我的**自定义" 选项卡**上的按钮以显示和隐藏操作窗格。

### <a name="to-test-the-custom-tab"></a>测试自定义选项卡

1. 按**F5**运行项目。

2. 选择 "**我的自定义选项**卡"。

3. 在 "**自定义操作窗格管理器**" 组中，选择 "**显示操作窗格 1**"。

     此时将显示 "操作" 窗格，并显示标签 "**操作窗格 1**"。

4. 选择 "**显示操作窗格 2**"。

     操作窗格将出现，并显示标签 "**操作窗格 2**"。

5. 选择 "**隐藏操作窗格**"。

     操作窗格不再可见。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Office 用户界面的更多信息：

- 将基于上下文的 UI 添加到任何文档级自定义项。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

- 扩展标准的或自定义的 Microsoft Office Outlook 窗体。 有关详细信息，请参见[演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)。

## <a name="see-also"></a>请参阅
- [在运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [自定义 Outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：自定义功能区入门](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：向 backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)
