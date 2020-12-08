---
title: 以编程方式自动填充增量变化的数据范围
description: 了解 Range 对象的自动填充方法如何允许您在工作表中自动填充值。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: dc80b4b589eb46aefa9ef6d75384ed17bb1b7c8c
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847203"
---
# <a name="how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data"></a>如何：以编程方式自动用递增变化的数据填充范围
  <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>使用对象的方法， <xref:Microsoft.Office.Interop.Excel.Range> 可以在工作表中自动填充值。 最常见的 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 方法是使用方法存储范围中递增或递减的值。 可以通过从枚举提供一个可选常量来指定行为 <xref:Microsoft.Office.Interop.Excel.XlAutoFillType> 。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 使用时，必须指定两个范围 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> ：

- 调用方法的范围 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> ，该范围指定填充的起始点并包含初始值。

- 要填充的范围，作为参数传递给 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 方法。 此目标范围必须包括包含初始值的范围。

    > [!NOTE]
    > 不能传递 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件来代替 <xref:Microsoft.Office.Interop.Excel.Range> 。 有关详细信息，请参阅 [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#49)]
 [!code-vb[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#49)]

## <a name="compile-the-code"></a>编译代码
 要填充的范围的第一个单元格必须包含初始值。

 该示例要求填充三个区域：

- B 列将包括5个工作日。 对于初始值，在单元格 B1 中键入 **星期一** 。

- C 列包含5个月。 对于初始值，请在 C1 单元格中键入 " **1 月** "。

- 列 D 将包含一系列数字，每行递增2。 对于初始值，在单元格 D2 的单元格 D1 和 **6** 中键入 **4** 。

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式在代码中引用工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式运行 Excel 计算](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
