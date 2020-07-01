---
title: 如何：以编程方式在工作表单元格中显示字符串
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], adding to worksheets
- worksheets, displaying text in cells
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ed93451942ccb0376c78ebb0e99b269a658131de
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545920"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>如何：以编程方式在工作表单元格中显示字符串
  此示例演示如何以编程方式在单元中显示文本。 若要在单元格中显示文本，请使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 此示例使用一个 <xref:Microsoft.Office.Tools.Excel.NamedRange> 名为的控件 `message` 。 必须在设计时将控件添加到文档级自定义项。 下面的代码必须置于 sheet 类中，而不是在 `ThisWorkbook` 类中。

### <a name="to-display-text-in-a-namedrange-control"></a>在 NamedRange 控件中显示文本

1. 将控件的值设置 <xref:Microsoft.Office.Tools.Excel.NamedRange> 为**Hello World**。

     [!code-csharp[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#68)]
     [!code-vb[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#68)]

## <a name="use-a-native-excel-range"></a>使用本机 Excel 范围
 下面的代码以编程方式创建一个新范围，然后为其赋值。

### <a name="to-display-text-in-an-excel-range"></a>显示 Excel 区域中的文本

1. 检索上单元格**A1**的范围 `Sheet1` ，并将值设置为**Hello World**。

     [!code-csharp[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#69)]
     [!code-vb[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#69)]

## <a name="see-also"></a>另请参阅
- [演练：使用 Windows 窗体收集数据](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [排查 Office 解决方案问题](../vsto/troubleshooting-office-solutions.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
