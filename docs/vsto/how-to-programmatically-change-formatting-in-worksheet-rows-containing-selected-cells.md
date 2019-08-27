---
title: 更改中包含通过代码的选定单元格的行的格式
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio]
- formatting [Office development in Visual Studio]
- worksheets, changing formatting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e77f555728ee89d7d202a35a91c9dbddba6224f3
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401382"
---
# <a name="how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells"></a>如何：以编程方式更改中包含选定单元格的工作表行的格式设置
  可以更改的整个行，包括所选单元格，使文本为粗体的字体。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-make-the-current-row-bold-and-the-previously-bolded-row-normal"></a>若要将当前行设置为粗体和正常以前粗体行

1. 声明一个静态变量以跟踪的以前所选的行。

    [!code-csharp[Trin_VstcoreExcelAutomation#37](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#37)]
    [!code-vb[Trin_VstcoreExcelAutomation#37](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#37)]

2. 检索对当前单元格使用引用<xref:Microsoft.Office.Interop.Excel._Application.ActiveCell%2A>属性。

    [!code-csharp[Trin_VstcoreExcelAutomation#38](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#38)]
    [!code-vb[Trin_VstcoreExcelAutomation#38](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#38)]

3. 当前行加粗使用样式<xref:Microsoft.Office.Interop.Excel.Range.EntireRow%2A>活动单元格的属性。

    [!code-csharp[Trin_VstcoreExcelAutomation#39](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#39)]
    [!code-vb[Trin_VstcoreExcelAutomation#39](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#39)]

4. 确保的当前值`previousRow`是不是 0。 0 （零） 表示这是首次执行此代码。

    [!code-csharp[Trin_VstcoreExcelAutomation#40](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#40)]
    [!code-vb[Trin_VstcoreExcelAutomation#40](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#40)]

5. 请确保当前行是不同于上一个行。

    [!code-csharp[Trin_VstcoreExcelAutomation#41](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#41)]
    [!code-vb[Trin_VstcoreExcelAutomation#41](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#41)]

6. 检索对表示以前选定的行的范围的引用并将该行不是粗体。

    [!code-csharp[Trin_VstcoreExcelAutomation#42](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#42)]
    [!code-vb[Trin_VstcoreExcelAutomation#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#42)]

7. 存储的当前行，以便它可以成为下一次通过上的上一个行。

    [!code-csharp[Trin_VstcoreExcelAutomation#43](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#43)]
    [!code-vb[Trin_VstcoreExcelAutomation#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#43)]

   以下示例显示完整的方法。

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#36](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#36)]
 [!code-vb[Trin_VstcoreExcelAutomation#36](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#36)]

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式复制数据和格式设置在工作表之间](../vsto/how-to-programmatically-copy-data-and-formatting-across-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
