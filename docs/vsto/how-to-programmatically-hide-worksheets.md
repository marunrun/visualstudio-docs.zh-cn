---
title: 如何：以编程方式隐藏工作表
description: 了解如何使用工作表主机项以编程方式显示或隐藏 Microsoft Excel 工作簿中的任何工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden worksheets
- worksheets, hiding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9a5ba61c7db0a62cf3e97fb8e4df5cb655e9f2dd
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525674"
---
# <a name="how-to-programmatically-hide-worksheets"></a>如何：以编程方式隐藏工作表
  可以显示或隐藏工作簿中的任意工作表。 若要隐藏工作表，请使用该工作表宿主项或通过使用工作簿的表集合访问该工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>使用工作表主机项
 如果在设计时将工作表添加到了文档级自定义项中，请使用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> 属性来隐藏指定的工作表。

### <a name="to-hide-a-worksheet-using-a-worksheet-host-item"></a>使用工作表宿主项隐藏工作表

1. 将 <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> 宿主项的 `Sheet1` 属性设置为 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> 枚举值。

     [!code-csharp[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#25)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合
 在下列情况中通过 Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Sheets> 集合访问工作表：

- 您希望隐藏 VSTO 外接程序中的工作表。

- 想要隐藏的工作表是在运行时在文档级自定义项中创建的。

### <a name="to-hide-a-worksheet-using-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合隐藏工作表

1. 将工作表的 <xref:Microsoft.Office.Interop.Excel.Worksheets.Visible%2A> 属性设置为 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> 枚举值。

     [!code-csharp[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#26)]

## <a name="see-also"></a>另请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式从工作簿中删除工作表](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [如何：以编程方式在工作簿中移动工作表](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
