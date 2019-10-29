---
title: 如何：将 ListObject 列映射到数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], mapping to ListObject column
- ListObject control, mapping data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cffd9f009d193f5ed687560b4f13940273fd82ad
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985896"
---
# <a name="how-to-map-listobject-columns-to-data"></a>如何：将 ListObject 列映射到数据
  将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件绑定到 <xref:System.Data.DataTable>时，可能不希望显示列表中的所有列，或可能具有未绑定到数据的特定列。 调用 <xref:Microsoft.Office.Tools.Excel.ListObject> 方法时，可以映射希望出现在 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 中的列。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="map-columns"></a>地图列

### <a name="to-map-a-data-table-to-columns-in-a-list"></a>将数据表映射到列表中的列

1. 在类级创建 <xref:System.Data.DataTable> 。

     [!code-csharp[Trin_VstcoreHostControlsExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#16)]
     [!code-vb[Trin_VstcoreHostControlsExcel#16](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#16)]

2. 在 `Sheet1` 类（文档级项目）或 `ThisAddIn` 类（在 VSTO 外接程序项目中）的 `Startup` 事件处理程序中添加示例列和数据。

     [!code-csharp[Trin_VstcoreHostControlsExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#17)]
     [!code-vb[Trin_VstcoreHostControlsExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#17)]

3. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 方法并以列名应显示的顺序传入列表。 List 对象将绑定到新创建的 <xref:System.Data.DataTable>，但列表对象中列的顺序将与它们在 <xref:System.Data.DataTable>中出现的顺序不同。

     [!code-csharp[Trin_VstcoreHostControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#18)]
     [!code-vb[Trin_VstcoreHostControlsExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#18)]

## <a name="specify-unmapped-columns"></a>指定未映射的列
 将列映射到 <xref:System.Data.DataTable>时，还可以通过传入空字符串来指定特定列不应绑定到数据。 未绑定到数据的新列随后会添加到 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。

### <a name="to-specify-an-unmapped-column-when-mapping-listobject-columns"></a>在映射 ListObject 列时指定未映射的列

1. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 方法并以列名应显示的顺序传入列表。 使用空字符串可指示添加未映射的列的位置；在此例中，是介于标题.栏与最后一个名称列之间。

     [!code-csharp[Trin_VstcoreHostControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs#19)]
     [!code-vb[Trin_VstcoreHostControlsExcel#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb#19)]

## <a name="compile-the-code"></a>编译代码
 此代码示例假定在此代码出现的工作表中有一个名为 <xref:Microsoft.Office.Tools.Excel.ListObject> 的现有 `list1` 。

## <a name="see-also"></a>请参阅
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：用数据填充 ListObject 控件](../vsto/how-to-fill-listobject-controls-with-data.md)
- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject 控件](../vsto/listobject-control.md)
