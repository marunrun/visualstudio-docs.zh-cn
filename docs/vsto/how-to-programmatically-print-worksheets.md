---
title: 如何：以编程方式打印工作表
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b0affdd34ad1cb302beacdc1abc9d02275878afd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537886"
---
# <a name="how-to-programmatically-print-worksheets"></a>如何：以编程方式打印工作表

可以打印工作簿中的任何工作表。

[!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="print-a-worksheet-in-a-document-level-customization"></a>打印文档级自定义项中的工作表

### <a name="to-print-a-worksheet"></a>打印工作表

1. 先调用 `Sheet1` 的 `PrintOut` 方法，请求两个副本，然后预览文档，再进行打印。

    [!code-csharp[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#22)]
    [!code-vb[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#22)]

   <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A>方法使您可以在 "**打印预览**" 窗口中显示指定的对象。 以下代码假定你已具有一个名为 `Sheet1` 的 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。

### <a name="to-preview-a-page-before-printing"></a>在打印之前预览页面

1. 调用工作表的 <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> 方法。

     [!code-csharp[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#23)]
     [!code-vb[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#23)]

## <a name="print-a-worksheet-in-a-vsto-add-in"></a>在 VSTO 外接程序中打印工作表

### <a name="to-print-a-worksheet"></a>打印工作表

1. 先调用活动工作表的 <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> 方法，请求两个副本，然后预览文档，再进行打印。

    [!code-csharp[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#14)]
    [!code-vb[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#14)]

   <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A>方法使您可以在 "**打印预览**" 窗口中显示指定的对象。

### <a name="to-preview-a-page-before-printing"></a>在打印之前预览页面

1. 调用活动工作表的 <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> 方法。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#15)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#15)]

## <a name="see-also"></a>另请参阅

- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式在工作表中检查拼写](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [工作表宿主项](../vsto/worksheet-host-item.md)
- [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
