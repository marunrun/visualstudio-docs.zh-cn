---
title: 如何：调整 NamedRange 控件的大小
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- NamedRange control, resizing
- ranges, resizing in Excel
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c57b3de77c2b32d7589fe50d55b3e81db08facd1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422487"
---
# <a name="how-to-resize-namedrange-controls"></a>如何：调整 NamedRange 控件的大小
  将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到 Microsoft Office Excel 文档时，可以设置该控件的大小；但是，你可能需要在以后调整其大小。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 在文档级项目中，可以在设计时或运行时调整命名范围的大小。 还可以在运行时在应用程序级 VSTO 外接程序中调整命名范围的大小。

 本主题介绍了以下任务：

- [在设计时调整 NamedRange 控件的大小](#designtime)

- [调整 NamedRange 控件在运行时在文档级项目中的大小](#runtimedoclevel)

- [调整 NamedRange 控件在运行时在 VSTO 外接程序项目中的大小](#runtimeaddin)

## <a name="designtime"></a> 在设计时调整 NamedRange 控件的大小
 可以通过在“定义名称”  对话框中重新定义其大小来调整命名范围的大小。

### <a name="to-resize-a-named-range-by-using-the-define-name-dialog-box"></a>使用“定义名称”对话框来调整命名范围的大小

1. 右击 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。

2. 在快捷菜单上单击“管理命名范围”  。

     “定义名称”  对话框随即出现。

3. 选择要调整大小的命名范围。

4. 清除 **引用** 框。

5. 选择要用来定义命名范围大小的单元格。

6. 单击 **“确定”**。

## <a name="runtimedoclevel"></a> 调整 NamedRange 控件在运行时在文档级项目中的大小
 可以通过编程的方式，使用 <xref:Microsoft.Office.Tools.Excel.NamedRange.RefersTo%2A> 属性调整命名范围的大小。

> [!NOTE]
> 在“属性”  窗口中， <xref:Microsoft.Office.Tools.Excel.NamedRange.RefersTo%2A> 属性标记为“只读”。

### <a name="to-resize-a-named-range-programmatically"></a>以编程方式调整命名范围大小

1. 在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 的单元格 **A1** 中创建一个 `Sheet1`控件。

     [!code-csharp[Trin_VstcoreHostControlsExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#4)]
     [!code-vb[Trin_VstcoreHostControlsExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#4)]

2. 调整命名范围的大小，使其包含单元格 **B1**。

     [!code-csharp[Trin_VstcoreHostControlsExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#5)]
     [!code-vb[Trin_VstcoreHostControlsExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#5)]

## <a name="runtimeaddin"></a> 调整 NamedRange 控件在运行时在 VSTO 外接程序项目中的大小
 可以调整大小<xref:Microsoft.Office.Tools.Excel.NamedRange>在运行时任何打开的工作表上的控件。 有关如何添加详细信息<xref:Microsoft.Office.Tools.Excel.NamedRange>VSTO 外接程序中使用控制到工作表，请参阅[如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)。

### <a name="to-resize-a-named-range-programmatically"></a>以编程方式调整命名范围大小

1. 在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 的单元格 **A1** 中创建一个 `Sheet1`控件。

     [!code-csharp[Trin_Excel_Dynamic_Controls#10](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#10)]
     [!code-vb[Trin_Excel_Dynamic_Controls#10](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#10)]

2. 调整命名范围的大小，使其包含单元格 **B1**。

     [!code-csharp[Trin_Excel_Dynamic_Controls#11](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#11)]
     [!code-vb[Trin_Excel_Dynamic_Controls#11](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#11)]

## <a name="see-also"></a>请参阅
- [扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [如何：调整书签控件的大小](../vsto/how-to-resize-bookmark-controls.md)
- [如何：调整 ListObject 控件的大小](../vsto/how-to-resize-listobject-controls.md)
