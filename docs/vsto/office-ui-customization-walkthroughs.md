---
title: Office UI 自定义演练
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes, walkthroughs
- smart documents, walkthroughs
- walkthroughs [Office development in Visual Studio], smart tags
- walkthroughs [Office development in Visual Studio], action panes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 95561f1404da1efd71ff3418f9154392f393795c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977882"
---
# <a name="office-ui-customization-walkthroughs"></a>Office UI 自定义演练
  下列演练演示了如何使用文档级自定义项和 VSTO 外接程序来自定义 Microsoft Office 应用程序的用户界面 (UI)。

## <a name="actions-pane-walkthroughs"></a>操作窗格演练
- [演练：从操作窗格的文档中插入文本](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)演示如何创建 Word 文档中的操作窗格。 操作窗格中包含可将用户输入发送到文档的两个控件。

- [演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)演示如何将操作窗格上的控件在 Word 中绑定到数据。 控件演示 SQL Server 数据库中表之间的主/从关系。

- [演练：将数据绑定到 Excel 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)描述如何添加绑定到数据源到 Excel 中的操作窗格的控件。

## <a name="custom-task-pane-walkthroughs"></a>自定义任务窗格演练
- [演练：自动执行应用程序从自定义任务窗格](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)演示如何创建包含在用户单击控件时自动执行宿主应用程序的自定义任务窗格。

- [演练：将自定义任务窗格与功能区按钮同步](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)演示如何创建用户可以隐藏或通过单击功能区上的切换按钮显示的自定义任务窗格。

- [演练：在 Outlook 中显示的电子邮件消息的自定义任务窗格](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)演示如何显示创建或打开在 Outlook 中的每封电子邮件的自定义任务窗格的唯一实例。

## <a name="ribbon-walkthroughs"></a>功能区演练
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)演示如何使用功能区设计器创建自定义功能区选项卡。 该选项卡包含一个用于隐藏或显示操作窗格的按钮。

- [演练：更新在运行时功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)演示了如何使用功能区对象模型在功能区加载到 Office 应用程序之后更新功能区上的控件。

- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)演示如何使用功能区 XML 而不是使用功能区设计器创建自定义功能区选项卡。

## <a name="controls-on-word-documents"></a>Word 文档中的控件
- [演练：在运行时在 VSTO 外接程序中向文档添加控件](../vsto/walkthrough-adding-controls-to-a-document-at-run-time-in-a-vsto-add-in.md)演示如何使用 VSTO 外接程序将控件添加到文档。

- [演练：更改文档格式设置使用 CheckBox 控件](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)演示如何更改 Word 文档中的文档级自定义项中使用复选框格式设置。

- [演练：在文本框中使用按钮在文档中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)演示了如何在 Word 文档中使用按钮和文本框。

- [演练：更新使用单选按钮在文档结构图](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)演示如何通过使用文档级自定义项中的选项按钮更改 Word 文档中的图表样式。

## <a name="controls-on-excel-worksheets"></a>Excel 工作表上的控件
- [演练：将控件添加到在运行时在 VSTO 外接程序项目中的工作表](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md)演示如何使用 VSTO 外接程序将控件添加到工作表。

- [演练：更改工作表格式设置使用 CheckBox 控件](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)演示使用 Excel 工作表上的复选框来更改格式设置的基础知识。

- [演练：在使用按钮的工作表中的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)演示使用 Excel 工作表上的按钮和文本框的基础知识。

- [演练：更新使用单选按钮的工作表中的图表](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)显示 Excel 工作表上使用选项按钮更改图表样式的基础知识。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Excel 用法演练](../vsto/walkthroughs-using-excel.md)
- [Office 解决方案演练中的数据](../vsto/data-in-office-solutions-walkthroughs.md)
- [安全和部署演练](../vsto/security-and-deployment-walkthroughs.md)
- [开始&#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
