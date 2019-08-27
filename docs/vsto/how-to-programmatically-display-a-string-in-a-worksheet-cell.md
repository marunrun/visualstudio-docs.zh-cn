---
title: 如何：以编程方式在工作表单元格中显示字符串
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: a9760d019fa80d4ecae63633c38ac9df60932202
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813018"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>如何：以编程方式在工作表单元格中显示字符串
  此示例演示如何以编程方式在单元格中显示文本。 若要在单元格中显示文本，请使用<xref:Microsoft.Office.Tools.Excel.NamedRange>控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 此示例使用<xref:Microsoft.Office.Tools.Excel.NamedRange>名为控件`message`。 该控件必须添加到在设计时为文档级自定义。 下面的代码必须放置在工作表类中，不在`ThisWorkbook`类。

### <a name="to-display-text-in-a-namedrange-control"></a>若要在 NamedRange 控件中显示文本

1. 设置的值<xref:Microsoft.Office.Tools.Excel.NamedRange>控制对**Hello World**。

     [!code-csharp[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#68)]
     [!code-vb[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#68)]

## <a name="use-a-native-excel-range"></a>使用本机 Excel 范围
 下面的代码以编程方式创建新的范围，然后将值分配到它。

### <a name="to-display-text-in-an-excel-range"></a>在 Excel 区域中显示文本

1. 在单元格的范围中检索**A1**上`Sheet1`并将值设置为**Hello World**。

     [!code-csharp[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#69)]
     [!code-vb[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#69)]

## <a name="see-also"></a>请参阅
- [演练：使用 Windows 窗体收集数据](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [对 Office 解决方案进行故障排除](../vsto/troubleshooting-office-solutions.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
