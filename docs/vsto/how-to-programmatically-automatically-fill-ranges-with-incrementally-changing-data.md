---
title: 以增量方式以编程方式更改数据范围的自动填充
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Autofill method [Excel]
- filling ranges automatically
- ranges, automatically filling
- workbooks, filling ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a514f83d12cd00c4a7792ae0bf2483fdd916897a
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177696"
---
# <a name="how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data"></a>如何：以编程方式自动用递增变化的数据填充范围
  <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>方法的<xref:Microsoft.Office.Interop.Excel.Range>对象，您可以自动使用值填充工作表中的范围。 大多数情况下，<xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>方法用于存储以增量方式增加或减少的范围内的值。 可以通过提供从一个可选常量指定行为<xref:Microsoft.Office.Interop.Excel.XlAutoFillType>枚举。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 使用时，必须指定两个范围<xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>:

- 调用区域<xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>方法，它指定填充的起始点并包含一个初始值。

- 你想要填充，范围作为参数传递给<xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>方法。 目标范围必须包括包含初始值的范围。

    > [!NOTE]
    > 不能将传递<xref:Microsoft.Office.Tools.Excel.NamedRange>控件来代替<xref:Microsoft.Office.Interop.Excel.Range>。 有关详细信息，请参阅[主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#49)]
 [!code-vb[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#49)]

## <a name="compile-the-code"></a>编译代码
 想要填充的范围的第一个单元必须包含一个初始值。

 该示例需要填充三个区域：

- B 列是包含 5 个工作日。 对于初始的值，请键入**星期一**单元格 B1 中。

- C 列是包含五个月。 对于初始的值，请键入**年 1 月**单元格 C1 中。

- 列 D 是包含一系列数字，每次递增两个用于每个行。 对于初始的值中，键入**4** D1 单元格中并**6** D2 单元格中。

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式引用在代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式运行 Excel 计算](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
