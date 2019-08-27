---
title: 如何：以编程方式选择工作表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, selecting
- Excel projects, selecting worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0b56df406049f3f4076f6e4d1efebcf0eb2abb18
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62962283"
---
# <a name="how-to-programmatically-select-worksheets"></a>如何：以编程方式选择工作表
  <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> 方法选择指定的对象，从而将用户的选择移到新对象上。 如果想要将焦点移到对象上，而不更改用户的选择，请使用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Activate%2A> 方法。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 如果你想要选择 VSTO 外接程序中的现有工作表，或者如果工作表在文档级自定义项中的运行时创建的你必须通过使用 Excel 访问它<xref:Microsoft.Office.Interop.Excel.Sheets>集合的 Excel 工作簿; 否则，可以访问<xref:Microsoft.Office.Tools.Excel.Worksheet>宿主项直接。

## <a name="use-the-worksheet-host-item"></a>使用工作表主机项
 文档级自定义项中，将以下代码添加到*Sheet1.vb*或*Sheet1.cs*。

### <a name="to-select-the-first-worksheet-in-a-workbook-using-a-host-item"></a>使用主机项选择工作簿中的第一个工作表

1. 调用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> 的 `Sheet1`方法。

     [!code-csharp[Trin_VstcoreExcelAutomation#19](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#19)]
     [!code-vb[Trin_VstcoreExcelAutomation#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#19)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合
 使用 Excel <xref:Microsoft.Office.Interop.Excel.Sheets> 集合访问工作表。

### <a name="to-select-the-first-worksheet-in-a-workbook-using-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的 Sheets 集合选择工作簿中的第一个工作表

1. 调用 <xref:Microsoft.Office.Interop.Excel.Sheets> 集合的 <xref:Microsoft.Office.Interop.Excel.Sheets.Select%2A> 方法来选择活动工作薄中的第一个工作表。

     [!code-csharp[Trin_VstcoreExcelAutomation#20](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#20)]
     [!code-vb[Trin_VstcoreExcelAutomation#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#20)]

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式打印工作表](../vsto/how-to-programmatically-print-worksheets.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [工作表主机项](../vsto/worksheet-host-item.md)
- [对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
