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
ms.openlocfilehash: e961479fc500e53133c62337478368878bf26893
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254127"
---
# <a name="office-ui-customization-walkthroughs"></a>Office UI 自定义演练
  下列演练演示了如何使用文档级自定义项和 VSTO 外接程序来自定义 Microsoft Office 应用程序的用户界面 (UI)。

## <a name="actions-pane-walkthroughs"></a>操作窗格演练
- [演练：从操作窗格](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)向文档中插入文本演示如何在 Word 文档中创建操作窗格。 操作窗格中包含可将用户输入发送到文档的两个控件。

- [演练：将数据绑定到 word 操作窗格](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)上的控件演示了如何将 Word 中操作窗格上的控件绑定到数据。 控件演示 SQL Server 数据库中表之间的主/从关系。

- [演练：将数据绑定到 excel 操作窗格](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)上的控件介绍了如何将绑定到数据源的控件添加到 excel 中的操作窗格。

## <a name="custom-task-pane-walkthroughs"></a>自定义任务窗格演练
- [演练：从自定义任务窗格](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)中自动执行应用程序演示如何创建自定义任务窗格，该窗格包含一个控件，该控件可在用户单击控件时自动执行宿主应用程序。

- [演练：将自定义任务窗格与功能区按钮](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)同步演示如何创建用户可以通过单击功能区上的切换按钮隐藏或显示的自定义任务窗格。

- [演练：使用 outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)中的电子邮件显示自定义任务窗格演示了如何使用在 Outlook 中创建或打开的每封电子邮件显示自定义任务窗格的唯一实例。

## <a name="ribbon-walkthroughs"></a>功能区演练
- [演练：使用功能区设计器](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)创建自定义选项卡演示了如何使用功能区设计器创建自定义功能区选项卡。 该选项卡包含一个用于隐藏或显示操作窗格的按钮。

- [演练：在运行时](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)更新功能区上的控件演示如何使用功能区对象模型在功能区加载到 Office 应用程序中之后更新功能区上的控件。

- [演练：使用功能区 xml](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)创建自定义选项卡演示如何使用功能区 xml 而不使用功能区设计器创建自定义功能区选项卡。

## <a name="controls-on-word-documents"></a>Word 文档中的控件
- [演练：在运行时在 vsto 外接程序](../vsto/walkthrough-adding-controls-to-a-document-at-run-time-in-a-vsto-add-in.md)中将控件添加到文档演示如何使用 VSTO 外接程序向文档中添加控件。

- [演练：使用 CheckBox 控件](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)更改文档格式演示如何使用文档级自定义项中的复选框来更改 Word 文档中的格式设置。

- [演练：使用按钮](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)在文档的文本框中显示文本演示如何在 Word 文档中使用按钮和文本框。

- [演练：使用单选按钮](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)更新文档中的图表演示如何使用文档级自定义项中的选项按钮更改 Word 文档中的图表样式。

## <a name="controls-on-excel-worksheets"></a>Excel 工作表上的控件
- [演练：在运行时在 vsto 外接程序项目](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md)中向工作表添加控件演示如何使用 vsto 外接程序将控件添加到工作表。

- [演练：使用 CheckBox 控件](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)更改工作表格式将演示使用 Excel 工作表上的复选框来更改格式设置的基础知识。

- [演练：使用按钮](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)在工作表的文本框中显示文本演示在 Excel 工作表上使用按钮和文本框的基础知识。

- [演练：使用单选按钮](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)更新工作表中的图表显示了在 Excel 工作表中使用选项按钮更改图表样式的基础知识。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
- [Office 解决方案演练中的数据](../vsto/data-in-office-solutions-walkthroughs.md)
- [安全和部署演练](../vsto/security-and-deployment-walkthroughs.md)
- [Visual Studio &#40;中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
