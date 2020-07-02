---
title: 如何：以编程方式列出工作簿中的所有工作表
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing worksheets
- worksheets, listing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 700aca059c6ef18f0c8e43aa127c99eaeee4fa2a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541448"
---
# <a name="how-to-programmatically-list-all-worksheets-in-a-workbook"></a>如何：以编程方式列出工作簿中的所有工作表
  <xref:Microsoft.Office.Interop.Excel.Workbook> 类提供一个 <xref:Microsoft.Office.Interop.Excel.Worksheets> 对象。 此对象包含工作簿中所有 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象的集合。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-document-level-customization"></a>在文档级自定义项中列出工作簿中所有现有的工作表

1. 循环访问 <xref:Microsoft.Office.Interop.Excel.Worksheets> 集合，将每个表的名称发送到通过 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件偏移的单元格。

     [!code-csharp[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#21)]
     [!code-vb[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#21)]

## <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-vsto-add-in"></a>若要列出 VSTO 外接程序中的工作簿中的所有现有工作表

1. 循环访问 <xref:Microsoft.Office.Interop.Excel.Worksheets> 集合，将每个表的名称发送到与 <xref:Microsoft.Office.Interop.Excel.Range> 对象偏移一定量的单元格。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#13)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#13)]

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式向工作簿添加新工作表](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式在工作簿中移动工作表](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
