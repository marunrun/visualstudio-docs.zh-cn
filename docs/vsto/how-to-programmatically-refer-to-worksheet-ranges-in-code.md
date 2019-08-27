---
title: 如何：以编程方式引用在代码中的工作表范围
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, referring to
- worksheets, referring to ranges
- referring to worksheet ranges
- Excel [Office development in Visual Studio], referring to worksheet ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2e82b884965c5c7362951c7d94199f90c93fbfc3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955948"
---
# <a name="how-to-programmatically-refer-to-worksheet-ranges-in-code"></a>如何：以编程方式引用在代码中的工作表范围
  使用类似的过程来指代的内容<xref:Microsoft.Office.Tools.Excel.NamedRange>控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 下面的示例添加<xref:Microsoft.Office.Tools.Excel.NamedRange>到工作表，然后向该范围中的单元格添加文本。

### <a name="to-refer-to-a-namedrange-control"></a>若要引用 NamedRange 控件

1. 将分配到的字符串<xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A>属性的<xref:Microsoft.Office.Tools.Excel.NamedRange>控件。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     [!code-csharp[Trin_VstcoreExcelAutomation#46](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#46)]
     [!code-vb[Trin_VstcoreExcelAutomation#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#46)]

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围
 下面的示例将本机 Excel 区域添加到工作表，然后到范围中的单元格添加文本。

### <a name="to-refer-to-a-native-range-object"></a>若要对本机范围对象，请参阅

1. 将分配到的字符串<xref:Microsoft.Office.Interop.Excel.Range.Value2%2A>范围的属性。

     [!code-csharp[Trin_VstcoreExcelAutomation#47](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#47)]
     [!code-vb[Trin_VstcoreExcelAutomation#47](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#47)]

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式检查工作表中的拼写](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式自动用递增变化的数据填充范围](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [如何：以编程方式搜索中工作表范围内的文本](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
