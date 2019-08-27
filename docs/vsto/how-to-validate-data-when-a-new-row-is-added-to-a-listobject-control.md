---
title: 在新行添加到 ListObject 控件时验证数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], validating data
- ListObject control, new row
- ListObject control, validating data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8cf302388b71174767d41cc8b1a7594f4223db2a
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328863"
---
# <a name="how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control"></a>如何：一个新行添加到 ListObject 控件时验证数据
  用户可以向绑定到数据的 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加新行。 可以在将更改提交到数据源之前验证用户数据。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="data-validation"></a>数据验证
 每当向绑定到数据的 <xref:Microsoft.Office.Tools.Excel.ListObject> 添加行时，便会引发 <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow> 事件。 可以处理此事件以执行数据验证。 例如，如果你的应用程序需要只有年龄在 18 岁与 65 岁之间的员工可以添加到数据源，验证添加行之前输入的年龄处于该范围内。

> [!NOTE]
> 除了在客户端上，还应始终在服务器上检查用户输入。 有关详细信息，请参阅[保护客户端应用程序](/dotnet/framework/data/adonet/secure-client-applications)。

### <a name="to-validate-data-when-a-new-row-is-added-to-data-bound-listobject"></a>在向数据绑定 ListObject 添加新行时验证数据

1. 在类级别为 ID 和 <xref:System.Data.DataTable> 创建变量。

     [!code-csharp[Trin_VstcoreHostControlsExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#8)]
     [!code-vb[Trin_VstcoreHostControlsExcel#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#8)]

2. 创建一个新<xref:System.Data.DataTable>并添加示例列和中的数据`Startup`事件处理程序`Sheet1`类 （在文档级项目中） 或`ThisAddIn`类 （在 VSTO 外接程序项目中）。

     [!code-csharp[Trin_VstcoreHostControlsExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#9)]
     [!code-vb[Trin_VstcoreHostControlsExcel#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#9)]

3. 向 `list1_BeforeAddDataBoundRow` 事件处理程序添加代码以检查输入的年龄是否处于可接受的范围内。

     [!code-csharp[Trin_VstcoreHostControlsExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#10)]
     [!code-vb[Trin_VstcoreHostControlsExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#10)]

## <a name="compile-the-code"></a>编译代码
 此代码示例假定在此代码出现的工作表中有一个名为 <xref:Microsoft.Office.Tools.Excel.ListObject> 的现有 `list1` 。

## <a name="see-also"></a>请参阅
- [扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ListObject 控件](../vsto/listobject-control.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：将 ListObject 列映射到数据](../vsto/how-to-map-listobject-columns-to-data.md)
