---
title: 如何：用数据填充 ListObject 控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnecting from data sources
- ListObject control, disconnecting from a data source
- ListObject control, filling with data
- data [Office development in Visual Studio], adding to worksheets
- data binding, ListObject controls
- worksheets, populating with data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f65f6de7cfb336eb001de47fb6562b7200391419
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967974"
---
# <a name="how-to-fill-listobject-controls-with-data"></a>如何：用数据填充 ListObject 控件
  可以使用数据绑定快速地将数据添加到文档中。 将数据绑定到列表对象后，可以断开列表对象的连接，以便它能显示数据且不再与数据源绑定。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：在连接到 SharePoint 列表的 Excel 中创建列表？](http://go.microsoft.com/fwlink/?LinkID=130263).

### <a name="to-bind-data-to-a-listobject-control"></a>将数据绑定到 ListObject 控件

1. 在类级创建 <xref:System.Data.DataTable> 。

     [!code-csharp[Trin_VstcoreHostControlsExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#20)]
     [!code-vb[Trin_VstcoreHostControlsExcel#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#20)]

2. 在 `Startup` 类（文档级项目中）或 `Sheet1` 类（应用程序级项目中）的 `ThisAddIn` 事件处理程序中添加示例列和数据。

     [!code-csharp[Trin_VstcoreHostControlsExcel#21](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#21)]
     [!code-vb[Trin_VstcoreHostControlsExcel#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#21)]

3. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 方法并以列名应显示的顺序传入列表。 列表对象中的列顺序可能与 <xref:System.Data.DataTable>中显示的列顺序不同。

     [!code-csharp[Trin_VstcoreHostControlsExcel#22](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#22)]
     [!code-vb[Trin_VstcoreHostControlsExcel#22](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#22)]

### <a name="to-disconnect-the-listobject-control-from-the-data-source"></a>若要断开 ListObject 控件与数据源的连接

1. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject.Disconnect%2A> 的 `List1`方法。

     [!code-csharp[Trin_VstcoreHostControlsExcel#23](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs#23)]
     [!code-vb[Trin_VstcoreHostControlsExcel#23](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb#23)]

## <a name="compile-the-code"></a>编译代码
 此代码示例假定在此代码出现的工作表中有一个名为 <xref:Microsoft.Office.Tools.Excel.ListObject> 的现有 `list1` 。

## <a name="see-also"></a>请参阅
- [扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：将 ListObject 列映射到数据](../vsto/how-to-map-listobject-columns-to-data.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject 控件](../vsto/listobject-control.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：用数据库中的数据填充工作表](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [如何：用服务中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)
