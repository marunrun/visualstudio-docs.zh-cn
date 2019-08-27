---
title: 存储和以编程方式检索在 Excel 范围内的日期值
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], retrieving date values from ranges
- ranges, retrieving data values
- dates, retrieving from Excel ranges
- Excel [Office development in Visual Studio], storing date values in ranges
- date values, storing in Excel ranges
- dates, storing in Excel ranges
- ranges, storing date values
- date values
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d855ffd91ccdc07a2d69401d7a8611175cc60941
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328925"
---
# <a name="how-to-programmatically-store-and-retrieve-date-values-in-excel-ranges"></a>如何：以编程方式存储和检索日期值在 Excel 范围内
  可以存储和检索中的值<xref:Microsoft.Office.Tools.Excel.NamedRange>控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 如果存储属于上或在范围内使用 Visual Studio 中的 Office 开发工具的 1/1/1900年之后的日期值，则将它存储在 OLE 自动化 (OA) 格式。 必须使用<xref:System.DateTime.FromOADate%2A>方法来检索其中的 OLE 自动化 (OA) 日期值。 如果日期早于 1900 年 1 月 1 日，则将它存储为字符串。

> [!NOTE]
> Excel 日期不同于 1900年前两个月的 OLE 自动化日期。 如果也会有差异**1904年日期系统**选项处于选中状态。 下面的代码示例不考虑这些差异。

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件

- 此示例适用于文档级自定义项。 下面的代码必须放置在工作表类中，不在`ThisWorkbook`类。

### <a name="to-store-a-date-value-in-a-named-range"></a>若要在命名范围中存储日期值

1. 创建<xref:Microsoft.Office.Tools.Excel.NamedRange>控件的单元格**A1**。

     [!code-csharp[Trin_VstcoreExcelAutomation#50](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#50)]
     [!code-vb[Trin_VstcoreExcelAutomation#50](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#50)]

2. 将今天的日期设置为值`NamedRange1`。

     [!code-csharp[Trin_VstcoreExcelAutomation#51](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#51)]
     [!code-vb[Trin_VstcoreExcelAutomation#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#51)]

### <a name="to-retrieve-a-date-value-from-a-named-range"></a>若要从命名范围中检索日期值

1. 检索日期值从`NamedRange1`。

     [!code-csharp[Trin_VstcoreExcelAutomation#52](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#52)]
     [!code-vb[Trin_VstcoreExcelAutomation#52](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#52)]

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围

### <a name="to-store-a-date-value-in-a-native-excel-range-object"></a>若要在本机 Excel 范围对象中存储日期值

1. 创建<xref:Microsoft.Office.Interop.Excel.Range>，表示单元格**A1**。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#25](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#25](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#25)]

2. 将今天的日期设置为值`rng`。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#26](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#26](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#26)]

### <a name="to-retrieve-a-date-value-from-a-native-excel-range-object"></a>若要从本机 Excel 范围对象中检索日期值

1. 检索日期值从`rng`。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#27](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#27)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#27](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#27)]

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：以编程方式引用在代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
