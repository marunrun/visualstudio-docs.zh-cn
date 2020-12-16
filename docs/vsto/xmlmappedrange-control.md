---
title: XmlMappedRange 控件
description: 了解 XmlMappedRange 控件是一个范围，该范围仅在非重复架构元素映射到 Microsoft Excel 中的单元格上时创建。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, data binding
- XMLMappedRange control
- XMLMappedRange control, events
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f3b3fd140787d44cdd8364ce77d5292dfcd83f54
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525897"
---
# <a name="xmlmappedrange-control"></a>XmlMappedRange 控件
  <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件是仅当非重复架构元素映射到 Microsoft Office Excel 中的单元格时创建的范围。 例如， `maxOccurs` 架构元素的属性等于1时。 在 Visual Studio 创建 XML 映射范围之后，可以直接对其进行编程，而无需遍历 Excel 对象模型。 删除元素映射后，只能删除 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> Excel 中的控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件支持绑定到单个数据字段 (简单的数据绑定) 。 <xref:Microsoft.Office.Tools.Excel.ListObject>控件可以支持复杂的数据绑定，当将重复架构元素映射到单元格时，将自动创建该控件。 有关详细信息，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>使用属性将控件绑定到数据源 <xref:System.Windows.Forms.Control.DataBindings%2A> 。 当 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 向工作表单元格添加时，Visual Studio 会自动从映射单元中的数据生成数据集，并将该控件绑定到该数据集。 的默认数据绑定属性 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 是 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Value2%2A> 。

 如果绑定数据集中的数据通过任何机制进行了更新，控件将 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 反映这些更改。

## <a name="formatting"></a>格式设置
 可以将相同的格式应用于 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 可应用于的控件 <xref:Microsoft.Office.Interop.Excel.Range> 。 这包括边框、字体、数字格式和样式。

## <a name="events"></a>事件
 可用于该控件的事件 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 包括：

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.SelectionChange>

## <a name="see-also"></a>另请参阅
- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：向工作表添加 XMLMappedRange 控件](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：将架构映射到 Visual Studio 内部的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
