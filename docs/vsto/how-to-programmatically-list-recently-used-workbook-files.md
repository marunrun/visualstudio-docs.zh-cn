---
title: 如何：以编程方式列出最近使用的工作簿文件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing recently used
- RecentFiles property
- Excel [Office development in Visual Studio], recently used files listing
- recent file list, Excel
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 954a106b87d0ee941aa9c3a6c9c35579d1cb3d54
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812529"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>如何：以编程方式列出最近使用的工作簿文件
  <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A>属性返回一个集合，包含显示最近使用的文件的 Microsoft Office Excel 列表中的所有文件的名称。 该列表的长度而异，具体取决于用户选择要保留的文件数量。 在范围内，可以显示结果。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>若要列出最近使用的工作簿范围对象中

1. 循环遍历的最近使用的文件列表，并将名称显示在单元格相对于<xref:Microsoft.Office.Interop.Excel.Range>对象。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#9)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#9)]

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
