---
title: 如何：以编程方式创建新工作簿
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], creating workbooks
- workbooks, creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 030bc801399ddcc73f145c0b45ca065c9a9ecc7a
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251876"
---
# <a name="how-to-programmatically-create-new-workbooks"></a>如何：以编程方式创建新工作簿
  以编程方式创建工作簿时，它是一个本机 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象，而不是 <xref:Microsoft.Office.Tools.Excel.Workbook> 主机项。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 你可以在 VSTO 外接程序项目中为 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象生成一个 <xref:Microsoft.Office.Tools.Excel.Workbook> 主机项。 有关详细信息，请参阅[在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="to-create-a-new-workbook"></a>创建新的工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> 集合的 <xref:Microsoft.Office.Interop.Excel.Workbooks> 方法。

     [!code-csharp[Trin_VstcoreExcelAutomation#1](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#1)]
     [!code-vb[Trin_VstcoreExcelAutomation#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#1)]

    > [!NOTE]
    > 通过将想要用作参数的模板传递给 <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> 方法，可以基于该模板而不是默认模板创建工作簿。

## <a name="see-also"></a>请参阅
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
