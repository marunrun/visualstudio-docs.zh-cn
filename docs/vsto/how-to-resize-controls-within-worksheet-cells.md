---
title: 如何：调整工作表单元格中的控件的大小
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- managed controls, resizing
- worksheets, resizing
- Windows Forms controls [Office development in Visual Studio], resizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b51f26a4ea2dec50c5ee90c38f49412866b6f866
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961486"
---
# <a name="how-to-resize-controls-within-worksheet-cells"></a>如何：调整工作表单元格中的控件的大小
  调整列或工作表上的行，单元格内的任何主机控件自动调整大小后的高度或宽度调整了大小的单元格。 默认情况下，Windows 窗体控件执行操作不自动调整。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 如果在设计时添加控件，则必须设置定位选项为每个控件。

 如果以编程方式添加 Windows 窗体控件，并提供了范围参数，该控件自动调整大小范围内的单元格重设大小时。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="resize-controls-at-design-time"></a>在设计时调整控件的大小

### <a name="to-make-controls-resize-with-cells-at-design-time"></a>若要使控件在设计时调整大小与单元格

1. 从**工具箱**，将 Windows 窗体控件拖到工作表。

2. 右键单击该控件，然后依次**格式控件**。

3. 在中**设置控件格式**对话框中，单击**属性**选项卡。

4. 下**对象定位**，选择**移动并调整其大小与单元格**选项，并单击**确定**。

     当调整包含该控件的单元格的大小时，该控件调整大小以适合该单元格。

## <a name="resize-controls-at-runtime"></a>调整控件在运行时的大小
 如果在运行时添加 Windows 窗体控件并传入<xref:Microsoft.Office.Interop.Excel.Range>用作控件的位置，该控件将自动调整大小重设大小时工作表包含的单元格范围。

### <a name="to-make-controls-resize-with-cells-at-run-time"></a>若要使控件在运行时调整大小与单元格

1. 将控件添加到 A1 的范围。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#5)]

     当调整包含该控件的单元格的大小时，该控件调整大小以适合该单元格。

## <a name="reset-control-placement"></a>控件位置重置
 你可以重置的位置和通过设置控件的大小调整`Placement`属性设置为下列任一<xref:Microsoft.Office.Interop.Excel.XlPlacement>值：

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>

### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>若要更改控件的行为，以便它不会重设大小或移动与该单元格

1. 调用控件的位置属性，并将值设置为<xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#6)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#6)]

## <a name="see-also"></a>请参阅
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [如何：打印时隐藏工作表上的控件](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office 文档上的 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
