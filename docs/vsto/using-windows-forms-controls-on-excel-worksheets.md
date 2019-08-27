---
title: 使用 Excel 工作表上的 Windows 窗体控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Windows Forms controls [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], Window Forms controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 032ee551ff04590ccdb8744c1274b137dec0b756
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982322"
---
# <a name="use-windows-forms-controls-on-excel-worksheets"></a>使用 Excel 工作表上的 Windows 窗体控件
  以相同方式向 Windows 窗体添加控件，可以向 Microsoft Office Excel 工作簿添加 Windows 窗体控件。 有关使用文档上的控件的常规信息，请参阅[Windows 窗体控件在 Office 文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="control-considerations-for-excel"></a>有关 Excel 控件注意事项
 有一些特定于 Excel 的几个注意事项。

### <a name="match-control-size-to-cell-size"></a>匹配控件大小与单元格大小
 可以将控件设置为当父单元格的大小更改时自动重设大小。 有关详细信息，请参阅[如何：调整工作表单元格中的控件的大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)。

### <a name="add-components-that-are-shared-by-all-worksheets"></a>添加由所有工作表共享的组件
 可以将希望在所有工作表之间共享的组件（如 <xref:System.Data.DataSet>）添加到工作簿设计器而不是工作表。 该组件将出现在组件栏中。

### <a name="formula-for-embedding-controls"></a>用于嵌入控件的公式
 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

## <a name="see-also"></a>请参阅
- [如何：调整工作表单元格中的控件的大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)
- [如何：打印时隐藏工作表上的控件](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [演练：更改工作表格式设置使用 CheckBox 控件](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)
- [演练：在使用按钮的工作表中的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)
- [演练：更新使用单选按钮的工作表中的图表](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)
