---
title: 如何：以编程方式对工作表中的行进行分组
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, creating groups
- groups, creating in worksheets
- ranges, creating groups
- worksheets, clearing groups
- groups
- groups [Office development in Visual Studio], clearing in worksheets
- worksheets, ungrouping rows and columns
- rows [Office development in Visual Studio], ungrouping
- columns [Office development in Visual Studio], ungrouping
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 759ba8c6e0796b25a87e8bf0b08795aed5bade05
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537873"
---
# <a name="how-to-programmatically-group-rows-in-a-worksheet"></a>如何：以编程方式对工作表中的行进行分组
  您可以对一个或多个整行进行分组。 若要在工作表中创建组，请使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 如果 <xref:Microsoft.Office.Tools.Excel.NamedRange> 在设计时将控件添加到文档级项目，则可以使用控件以编程方式创建组。 下面的示例假定 <xref:Microsoft.Office.Tools.Excel.NamedRange> 同一工作表上有三个控件： `data2001` 、 `data2002` 和 `dataAll` 。 每个命名范围引用工作表中的一个整行。

### <a name="to-create-a-group-of-namedrange-controls-on-a-worksheet"></a>在工作表上创建一组 NamedRange 控件

1. 通过调用每个范围的方法，将三个命名范围分组 <xref:Microsoft.Office.Tools.Excel.NamedRange.Group%2A> 。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     [!code-csharp[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#32)]
     [!code-vb[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#32)]

    > [!NOTE]
    > 若要取消行的分组，请调用 <xref:Microsoft.Office.Tools.Excel.NamedRange.Ungroup%2A> 方法。

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围
 此代码假定 `data2001` `data2002` 工作表上有三个名为、和的 Excel 范围 `dataAll` 。

### <a name="to-create-a-group-of-excel-ranges-in-a-worksheet"></a>在工作表中创建一组 Excel 范围

1. 通过调用每个范围的方法，将三个命名范围分组 <xref:Microsoft.Office.Interop.Excel.Range.Group%2A> 。 下面的示例假定在 <xref:Microsoft.Office.Interop.Excel.Range> `data2001` `data2002` `dataAll` 同一工作表上有三个名为、和的控件。 每个命名范围引用工作表中的一个整行。

     [!code-csharp[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#33)]
     [!code-vb[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#33)]

    > [!NOTE]
    > 若要取消行的分组，请调用 <xref:Microsoft.Office.Interop.Excel.Range.Ungroup%2A> 方法。

## <a name="see-also"></a>另请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
