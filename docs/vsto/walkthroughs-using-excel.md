---
title: Excel 用法演练
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- walkthroughs [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], walkthroughs
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4d6c092daf02ccd6546621fbeff3422cd87fb0db
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62947826"
---
# <a name="walkthroughs-using-excel"></a>Excel 用法演练
  下列演练演示了使用文档级自定义项和 VSTO 外接程序来自动化 Microsoft Office Excel 和自定义用户界面 (UI) 的方式。

## <a name="document-level-walkthroughs"></a>文档级演练
- [演练：创建在第一个文档级自定义 excel](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)演示了如何为 Excel 创建基本文档级自定义。

- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)演示如何向 Excel 工作簿的功能区添加自定义选项卡。

- [演练：使用 Windows 窗体收集数据](../vsto/walkthrough-collecting-data-using-a-windows-form.md)说明了使用 Windows 窗体来收集用户输入，然后将输入发送到一个单元格的 Excel 工作表中。

- [演练：更改工作表格式设置使用 CheckBox 控件](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)演示使用 Excel 工作表上的复选框来更改格式设置的基础知识。

- [演练：在使用按钮的工作表中的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)演示使用 Excel 工作表上的按钮和文本框的基础知识。

- [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)分步说明了如何添加<xref:Microsoft.Office.Tools.Excel.NamedRange>对工作表和对其事件进行编程控制。

- [演练：在文档级项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)演示将 SQL Server 数据库中的单个数据字段绑定到 Excel 中的命名范围的基础知识。

- [演练：在文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)演示绑定到 Northwind SQL Server 数据库中的字段的 Excel 工作表中的多个单元格的基础知识。

- [演练：创建使用缓存的数据集的主从关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)演示如何在工作表上创建主/从关系以及缓存数据，以便可以脱机使用该解决方案。

- [演练：更新使用单选按钮的工作表中的图表](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)显示 Excel 工作表上使用单选按钮更改图表样式的基础知识。

- [演练：将数据绑定到 Excel 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)描述如何添加绑定到数据源到 Excel 中的操作窗格的控件。

## <a name="application-level-walkthroughs"></a>应用程序级演练
- [演练：创建第一个 VSTO 外接程序 Excel](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)演示了如何为 Excel 创建基本 VSTO 外接程序中。

- [演练：将控件添加到在运行时在 VSTO 外接程序项目中的工作表](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md)演示如何使用 VSTO 外接程序将控件添加到工作表。

- [演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)演示如何公开 VSTO 外接程序中向工作簿中的 VBA 代码的对象。

- [演练：将自定义任务窗格与功能区按钮同步](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)演示如何创建用户可以隐藏或通过单击功能区上的切换按钮显示的自定义任务窗格。

- [演练：VSTO 外接程序项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)演示如何将表绑定到 SQL Server 数据库中<xref:Microsoft.Office.Tools.Excel.ListObject>VSTO 外接程序中的 Excel。
