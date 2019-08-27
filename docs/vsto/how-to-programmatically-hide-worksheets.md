---
title: 如何：以编程方式隐藏工作表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden worksheets
- worksheets, hiding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f1fca54350900b2ed252efc324308d1168c6da53
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812458"
---
# <a name="how-to-programmatically-hide-worksheets"></a>如何：以编程方式隐藏工作表
  可以显示或隐藏工作簿中的任意工作表。 若要隐藏工作表，请使用该工作表宿主项或通过使用工作簿的表集合访问该工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>使用工作表主机项
 如果在设计时将工作表添加到了文档级自定义项中，请使用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> 属性来隐藏指定的工作表。

### <a name="to-hide-a-worksheet-using-a-worksheet-host-item"></a>使用工作表宿主项隐藏工作表

1. 将 <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> 宿主项的 `Sheet1` 属性设置为 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> 枚举值。

     [!code-csharp[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#25)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合
 在下列情况中通过 Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Sheets> 集合访问工作表：

- 你想要隐藏 VSTO 外接程序中的工作表。

- 想要隐藏的工作表是在运行时在文档级自定义项中创建的。

### <a name="to-hide-a-worksheet-using-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合隐藏工作表

1. 将工作表的 <xref:Microsoft.Office.Interop.Excel.Worksheets.Visible%2A> 属性设置为 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> 枚举值。

     [!code-csharp[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#26)]

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式移动工作簿内的工作表](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
