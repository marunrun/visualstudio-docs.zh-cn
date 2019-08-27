---
title: 如何：以编程方式将样式应用于工作簿中的范围
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, styles
- styles, workbook ranges
- workbooks, styles
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f74b2d08a268bc79bcd7d2fd33513b5ccf5b1415
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817448"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>如何：以编程方式将样式应用于工作簿中的范围
  可以将已命名的样式应用到工作簿中的区域。 Excel 提供了大量预定义样式。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 **“设置单元格格式”** 对话框显示了可用于设置单元格格式的所有选项，且其中每个选项都可从你的代码获取。 若要在 Excel 中显示此对话框，请单击 **“格式”** 菜单上的 **“单元格”** 。

## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>将样式应用到文档级自定义项中的命名区域

1. 创建一个新样式并设置其属性。

     [!code-csharp[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#53)]
     [!code-vb[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#53)]

2. 创建一个 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件，向其分配文本，然后应用新样式。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     [!code-csharp[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#54)]
     [!code-vb[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#54)]

## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>从文档级自定义项的命名区域中清除样式

1. 将正文样式应用到该区域中。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     [!code-csharp[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#55)]
     [!code-vb[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#55)]

## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>将样式应用到 VSTO 外接程序中的命名区域

1. 创建一个新样式并设置其属性。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#28)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#28)]

2. 创建一个 <xref:Microsoft.Office.Interop.Excel.Range>，对其分配文本，然后应用新样式。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#29)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#29)]

## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>若要从 VSTO 外接程序中的命名区域清除样式

1. 将正文样式应用到该区域中。

     [!code-csharp[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#56)]
     [!code-vb[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#56)]

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
