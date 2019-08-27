---
title: 如何：以编程方式将颜色应用于 Excel 范围
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- color, Excel ranges
- ranges, applying color
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 56ecbfcdaf22132f63df1ecf5eadba97dee426af
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817268"
---
# <a name="how-to-programmatically-apply-color-to-excel-ranges"></a>如何：以编程方式将颜色应用于 Excel 范围
  若要将颜色应用于单元格的范围内的文本，请使用<xref:Microsoft.Office.Tools.Excel.NamedRange>控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 此示例适用于文档级自定义项。

### <a name="to-apply-color-to-a-namedrange-control"></a>若要将颜色应用于 NamedRange 控件

1. 创建<xref:Microsoft.Office.Tools.Excel.NamedRange>A1 单元格中的控件。

     [!code-csharp[Trin_VstcoreExcelAutomation#65](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#65)]
     [!code-vb[Trin_VstcoreExcelAutomation#65](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#65)]

2. 设置中的文本的颜色<xref:Microsoft.Office.Tools.Excel.NamedRange>控件。

     [!code-csharp[Trin_VstcoreExcelAutomation#66](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#66)]
     [!code-vb[Trin_VstcoreExcelAutomation#66](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#66)]

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围

### <a name="to-apply-color-to-a-native-excel-range-object"></a>若要将颜色应用于本机 Excel 范围对象

1. 创建于单元格 A1 的范围，然后设置文本的颜色。

     [!code-csharp[Trin_VstcoreExcelAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#67)]
     [!code-vb[Trin_VstcoreExcelAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#67)]

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式引用在代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
