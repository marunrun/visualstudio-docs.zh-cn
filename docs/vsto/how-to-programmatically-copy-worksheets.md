---
title: 如何：以编程方式复制工作表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying
- Excel [Office development in Visual Studio], copying worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 17d248fb0805c83feb64b2f0a28a645b1fa29d49
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422497"
---
# <a name="how-to-programmatically-copy-worksheets"></a>如何：以编程方式复制工作表
  你可以创建一份工作表的副本，并将该工作表插入工作簿中现有的工作表之前或之后。 如果不指定要插入工作表的位置，则 Excel 将创建一个新的工作簿来容纳新工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

> [!NOTE]
> 无论是以编程方式复制工作表，还是最终用户手动复制工作表，新工作表都没有代码，并且新工作表上的控件无法运行。 这是因为新复制的工作表是 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象而不 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。 Windows 窗体控件和主机控件仅可以添加到主机项。 有关详细信息，请参阅[主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-document-level-customization"></a>将复制的工作表添加到文档级自定义项中的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> 方法复制当前工作簿中的第一个工作表并将副本放在第三个工作表后。

     [!code-csharp[Trin_VstcoreExcelAutomation#16](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#16)]
     [!code-vb[Trin_VstcoreExcelAutomation#16](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#16)]

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-vsto-add-in"></a>将复制的工作表添加到 VSTO 外接程序中的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> 方法复制当前工作簿中的第一个工作表并将副本放在第三个工作表后。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#12](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#12)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#12](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#12)]

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [如何：以编程方式将新工作表添加到工作簿](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式选择工作表](../vsto/how-to-programmatically-select-worksheets.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
