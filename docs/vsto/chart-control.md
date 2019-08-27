---
title: 图表控件
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.ExcelChart
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], events
- Chart control [Office development in Visual Studio]
- Chart control [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 21ca64f6661c4f0d7182bf20887ff8bdf754a6fc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440315"
---
# <a name="chart-control"></a>图表控件
  <xref:Microsoft.Office.Tools.Excel.Chart> 控件是公开事件的图表对象。 当将图表添加到工作表时，Visual Studio 将创建 <xref:Microsoft.Office.Tools.Excel.Chart> 对象，你可以直接针对此对象编程而无需遍历 Microsoft Office Excel 对象模型。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>创建控件
 您可以添加<xref:Microsoft.Office.Tools.Excel.Chart>到 Microsoft Office Excel 工作表在设计时或在运行时在文档级项目中的控件。

 您可以添加<xref:Microsoft.Office.Tools.Excel.Chart>向在 VSTO 外接程序中的运行时工作表中的控件。 有关详细信息，请参阅[如何：将图表控件添加到工作表](../vsto/how-to-add-chart-controls-to-worksheets.md)。

> [!NOTE]
> 工作表关闭时，动态创建的图表控件不作为主机控件保留在工作表中。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="formatting"></a>格式化
 可应用于 <xref:Microsoft.Office.Interop.Excel.Chart> 的所有格式设置也可应用于 <xref:Microsoft.Office.Tools.Excel.Chart> 控件。 这包括边框、字体、图表类型、网格线、图例和数据标签。

## <a name="events"></a>事件
 以下事件可用于 <xref:Microsoft.Office.Tools.Excel.Chart> 控件：

- <xref:Microsoft.Office.Tools.Excel.Chart.ActivateEvent>

- <xref:Microsoft.Office.Tools.Excel.Chart.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.Chart.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.Chart.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.Chart.Calculate>

- <xref:Microsoft.Office.Tools.Excel.Chart.Deactivate>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.Chart.DragOver>

- <xref:Microsoft.Office.Tools.Excel.Chart.DragPlot>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseDown>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseMove>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseUp>

- <xref:Microsoft.Office.Tools.Excel.Chart.Resize>

- <xref:Microsoft.Office.Tools.Excel.Chart.SelectEvent>

- <xref:Microsoft.Office.Tools.Excel.Chart.SeriesChange>

## <a name="see-also"></a>请参阅
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：将图表控件添加到工作表](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
