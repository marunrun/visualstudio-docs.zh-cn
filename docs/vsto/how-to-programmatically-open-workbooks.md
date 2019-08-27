---
title: 如何：以编程方式打开工作簿
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening
- Excel [Office development in Visual Studio], opening workbooks
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: facf3cbeb6635324e74244983fcb33138ad64cfe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812369"
---
# <a name="how-to-programmatically-open-workbooks"></a>如何：以编程方式打开工作簿
  <xref:Microsoft.Office.Interop.Excel.Workbooks> Microsoft Office Excel 中的集合就可以使用所有打开的工作簿并打开工作簿。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-open-an-existing-workbook"></a>若要打开现有的工作簿

1. 使用<xref:Microsoft.Office.Interop.Excel.Workbooks.Open%2A>方法的<xref:Microsoft.Office.Interop.Excel.Workbooks>集合，在路径中将传递给该工作簿。

     [!code-csharp[Trin_VstcoreExcelAutomation#2](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreExcelAutomation#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#2)]

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 名为工作簿`YourWorkbook.xls`必须存在于一个名为目录`Test`在驱动器 c。

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式将文本文件打开为工作簿](../vsto/how-to-programmatically-open-text-files-as-workbooks.md)
- [如何：以编程方式创建新的工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
