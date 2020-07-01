---
title: 如何：以编程方式运行 Excel 计算
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, running calculations
- calculations, running in Excel
- Excel [Office development in Visual Studio], running calculations programmatically
- workbooks, running calculations
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a02e86864065d2c626de2f6e7fea7528554f1391
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547376"
---
# <a name="how-to-programmatically-run-excel-calculations"></a>如何：以编程方式运行 Excel 计算
  您可以使用类似的过程在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象中运行计算。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="run-calculations-in-a-namedrange-control"></a>在 NamedRange 控件中运行计算
 下面的示例 <xref:Microsoft.Office.Tools.Excel.NamedRange> 在单元格 A1 中创建一个，然后计算单元。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

### <a name="to-run-calculations-in-a-namedrange-control"></a>在 NamedRange 控件中运行计算

1. 创建命名范围。

     [!code-csharp[Trin_VstcoreExcelAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#75)]
     [!code-vb[Trin_VstcoreExcelAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#75)]

2. 调用 <xref:Microsoft.Office.Tools.Excel.NamedRange.Calculate%2A> 指定范围的方法。

     [!code-csharp[Trin_VstcoreExcelAutomation#76](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#76)]
     [!code-vb[Trin_VstcoreExcelAutomation#76](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#76)]

## <a name="run-calculations-in-a-native-excel-range"></a>在本机 Excel 范围中运行计算

### <a name="to-run-calculations-in-a-native-excel-range"></a>在本机 Excel 范围中运行计算

1. 创建命名范围。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#30](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#30)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#30](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#30)]

2. 调用 <xref:Microsoft.Office.Interop.Excel.Range.Calculate%2A> 指定范围的方法。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#31](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#31)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#31](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#31)]

## <a name="see-also"></a>另请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
