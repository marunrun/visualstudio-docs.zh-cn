---
title: ListObject 控件
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.List
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- lists, events
- ListObject control
- ListObject control, events
- ListObject control, data binding
- ListObject control, improving performance when bound to data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3b5286a4bddff2b529abd0a565bb4dbeef7ffaf3
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251869"
---
# <a name="listobject-control"></a>ListObject 控件
  <xref:Microsoft.Office.Tools.Excel.ListObject> 控件是公开事件并且可以绑定到数据的列表。 当将列表添加到工作表时，Visual Studio 将创建 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件，你可以直接针对此控件编程而无需遍历 Microsoft Office Excel 对象模型。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>创建控件
 在文档级项目中，可以在设计时或运行时向工作表中添加 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。 在 VSTO 外接程序项目中，只能在运行时向工作表添加 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。 有关详细信息，请参阅[如何：将 ListObject 控件添加到](../vsto/how-to-add-listobject-controls-to-worksheets.md)工作表。

> [!NOTE]
> 默认情况下，工作表关闭时，动态创建的列表对象不作为宿主控件保留在工作表中。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件支持简单和复杂数据绑定。 可以在设计时使用 <xref:Microsoft.Office.Tools.Excel.ListObject> 和 <xref:Microsoft.Office.Tools.Excel.ListObject.DataSource%2A> 属性或在运行时使用 <xref:Microsoft.Office.Tools.Excel.ListObject.DataMember%2A> 方法将 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 控件绑定到数据源。

> [!NOTE]
> 当 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到在数据更改时会引发事件的数据源（如 <xref:System.Data.DataTable>）时，它会自动更新。 如果将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到在数据更改时不会引发事件的数据源，则必须调用 <xref:Microsoft.Office.Tools.Excel.ListObject.RefreshDataRow%2A> 或 <xref:Microsoft.Office.Tools.Excel.ListObject.RefreshDataRows%2A> 方法以更新 <xref:Microsoft.Office.Tools.Excel.ListObject>。

 通过将重复架构元素映射到工作表单元格来将 <xref:Microsoft.Office.Tools.Excel.ListObject> 添加到该单元格时，Visual Studio 会自动将 <xref:Microsoft.Office.Tools.Excel.ListObject> 映射到生成的数据集。 但是， <xref:Microsoft.Office.Tools.Excel.ListObject> 不会自动绑定到数据。 在文档级项目中，可以执行相应步骤以在设计时或运行时将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到数据集。 在 VSTO 外接程序<xref:Microsoft.Office.Tools.Excel.ListObject>中，可以在运行时以编程方式将绑定到数据集。

 因为数据与 <xref:Microsoft.Office.Tools.Excel.ListObject>分离，所以应通过绑定数据集添加和删除数据，而不是直接通过 <xref:Microsoft.Office.Tools.Excel.ListObject>。 如果绑定数据集中的数据通过任何机制进行了更新，那么 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件会自动反映这些变化。 有关详细信息，请参阅[将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

 可以通过将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到数据源来快速填充 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。 如果在数据绑定 <xref:Microsoft.Office.Tools.Excel.ListObject>中编辑数据，则也会在数据源中自动进行更改。 如果要填充 <xref:Microsoft.Office.Tools.Excel.ListObject> ，然后使用户可以更改 <xref:Microsoft.Office.Tools.Excel.ListObject> 中的数据而无需修改数据源，则可以使用 <xref:Microsoft.Office.Tools.Excel.ListObject.Disconnect%2A> 方法将 <xref:Microsoft.Office.Tools.Excel.ListObject> 从数据源分离。 有关详细信息，请参阅[如何：用数据](../vsto/how-to-fill-listobject-controls-with-data.md)填充 ListObject 控件。

> [!NOTE]
> 重叠 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件不支持数据绑定。

### <a name="improve-performance-in-listobject-controls"></a>提高 ListObject 控件中的性能
 如果先绑定控件，然后调用 <xref:Microsoft.Office.Tools.Excel.ListObject> 以填充数据集，则将 XML 文件读取到数据绑定 <xref:System.Data.DataSet.ReadXml%2A> 控件中的过程倾向于越来越慢。 要改进性能，请在绑定控件之前调用 <xref:System.Data.DataSet.ReadXml%2A> 。

### <a name="disconnect-listobject-controls-from-the-data-source"></a>断开 ListObject 控件与数据源的连接
 通过将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件绑定到数据源来使用数据填充它之后，可以对它断开连接，以便对列表对象中的数据进行的修改不会影响数据源。 有关详细信息，请参阅[如何：用数据](../vsto/how-to-fill-listobject-controls-with-data.md)填充 ListObject 控件。

### <a name="restore-column-and-row-order"></a>还原列和行顺序
 如果数据绑定到已在设计时添加到文档的 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件，则只要保存工作簿，Visual Studio 便会跟踪列和行顺序。 如果用户在运行时移动 <xref:Microsoft.Office.Tools.Excel.ListObject> 列或行，则在下次打开工作簿并且 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件再次绑定到数据源时，新顺序会保留。

 如果要将 <xref:Microsoft.Office.Tools.Excel.ListObject> 还原为其原始列和行顺序，则可以调用 <xref:Microsoft.Office.Tools.Excel.ListObject.ResetPersistedBindingInformation%2A> 方法。 此方法会删除与指定 <xref:Microsoft.Office.Tools.Excel.ListObject>的列和行顺序相关的自定义文档属性。 如果不想保留 <xref:Microsoft.Office.Tools.Excel.Workbook.Shutdown> 的列和行顺序，请从工作簿的 <xref:Microsoft.Office.Tools.Excel.ListObject>事件调用此方法。

## <a name="format"></a>格式
 可应用于 <xref:Microsoft.Office.Interop.Excel.ListObject> 的格式设置也可应用于 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。 这包括边框、字体、数字格式和样式。 最终用户可以在数据绑定<xref:Microsoft.Office.Tools.Excel.ListObject>中重新排列列，这些更改会随文档保留， <xref:Microsoft.Office.Tools.Excel.ListObject>前提是在设计时添加到文档中。 下次打开文档时，列表对象会绑定到同一个数据源，但是列顺序会反映用户的更改。

## <a name="add-and-remove-columns-at-run-time"></a>在运行时添加和删除列
 无法在运行时手动添加或删除数据绑定 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件中的列。 如果最终用户尝试删除某列，则它会立即还原，并且添加的所有列都将被删除。 因此，需编写代码来向用户说明为何无法对绑定到数据的 <xref:Microsoft.Office.Tools.Excel.ListObject> 执行这些操作，这十分重要。 Visual Studio 在与数据绑定相关的 <xref:Microsoft.Office.Tools.Excel.ListObject> 上提供了多个事件。 例如，可以使用 <xref:Microsoft.Office.Tools.Excel.ListObject.OriginalDataRestored> 事件来警告用户，他们尝试删除的数据无法删除，已还原。

## <a name="add-and-remove-rows-at-run-time"></a>在运行时添加和删除行
 可以手动添加和删除数据绑定 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件中的行（前提是数据源允许添加新行，并且不是只读的）。 可以针对诸如 <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow> 这类事件编写代码以验证数据。 有关详细信息，请参阅[如何：向 ListObject 控件](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)添加新行时验证数据。

 列表对象与数据源的关系有时会导致例程错误。 例如，可以映射要在 <xref:Microsoft.Office.Tools.Excel.ListObject>中显示的列，因此如果省略具有限制的列（例如不能接受 null 值的字段），则每次创建行时都会引发错误。 可以编写代码以在 <xref:Microsoft.Office.Tools.Excel.ListObject.ErrorAddDataBoundRow> 事件的事件处理程序中添加缺少的值。

## <a name="rename-listobject-controls-in-excel"></a>在 Excel 中重命名 ListObject 控件
 Excel 使用户可以使用“设计” 选项卡在运行时更改 Excel 表的名称。但是， <xref:Microsoft.Office.Tools.Excel.ListObject> 控件不支持此功能。 如果用户尝试重命名与 <xref:Microsoft.Office.Tools.Excel.ListObject>对应的 Excel 表，则 Excel 表的名称会在保存工作簿时自动恢复为原始名称。

## <a name="events"></a>事件
 以下事件可用于 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件：

- <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow>

- <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.ListObject.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.ListObject.Change>

- <xref:Microsoft.Office.Tools.Excel.ListObject.DataBindingFailure>

- <xref:Microsoft.Office.Tools.Excel.ListObject.DataMemberChanged>

- <xref:Microsoft.Office.Tools.Excel.ListObject.DataSourceChanged>

- <xref:Microsoft.Office.Tools.Excel.ListObject.Deselected>

- <xref:Microsoft.Office.Tools.Excel.ListObject.ErrorAddDataBoundRow>

- <xref:Microsoft.Office.Tools.Excel.ListObject.OriginalDataRestored>

- <xref:Microsoft.Office.Tools.Excel.ListObject.Selected>

- <xref:Microsoft.Office.Tools.Excel.ListObject.SelectedIndexChanged>

- <xref:Microsoft.Office.Tools.Excel.ListObject.SelectionChange>

## <a name="see-also"></a>请参阅
- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：将 ListObject 控件添加到工作表](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [如何：调整 ListObject 控件的大小](../vsto/how-to-resize-listobject-controls.md)
- [如何：向 ListObject 控件添加新行时验证数据](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)
- [如何：将 ListObject 列映射到数据](../vsto/how-to-map-listobject-columns-to-data.md)
- [如何：用数据填充 ListObject 控件](../vsto/how-to-fill-listobject-controls-with-data.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：使用数据库中的数据填充工作表](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
