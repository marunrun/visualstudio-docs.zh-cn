---
title: 复制数据和以编程方式在工作表之间格式设置
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: b90704d6d9fe555920fb042939079bd53884cfbe
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402210"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>如何：以编程方式复制数据和格式设置在工作表之间
  您可以将数据复制从上一个工作表范围到工作簿中的所有其他表使用<xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A>方法。 指定的范围，以及是否要将复制数据、 格式设置，或两者。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#44)]
 [!code-vb[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#44)]

## <a name="compile-the-code"></a>编译代码
 此示例需要名为一个范围`rangeData`工作表中。

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式将新工作表添加到工作簿](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式更改中包含选定单元格的工作表行的格式设置](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
