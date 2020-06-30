---
title: 以编程方式在工作表之间复制数据和格式设置
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying data
- formatting [Office development in Visual Studio]
- data [Office development in Visual Studio], copying across worksheets
- copying data, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 07baa23b6fd276e8fb8452934dc6361544d16038
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546102"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>如何：以编程方式在工作表之间复制数据和格式设置
  您可以使用方法将数据从一个工作表中的一个范围复制到工作簿中的所有其他表 <xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A> 。 指定一个范围，以及是要复制数据、设置格式还是同时复制两者。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#44)]
 [!code-vb[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#44)]

## <a name="compile-the-code"></a>编译代码
 此示例需要 `rangeData` 在工作表中指定一个范围。

## <a name="see-also"></a>另请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式向工作簿添加新工作表](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式在包含选定单元格的工作表行中更改格式设置](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
