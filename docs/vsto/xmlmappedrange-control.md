---
title: XmlMappedRange 控件
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
ms.openlocfilehash: cde5489d970de02afbce28ab9c60c677ab199c84
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810744"
---
# <a name="xmlmappedrange-control"></a>XmlMappedRange 控件
  <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件是仅在非重复架构元素映射到 Microsoft Office Excel 中的单元格上时创建一个范围。 例如，当`maxOccurs`架构元素的特性等于 1。 Visual Studio 将创建 XML 映射范围后，你可以针对它编程直接而无需遍历 Excel 对象模型。 您只能删除<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>中移除的元素映射时，在 Excel 内的控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：在 Excel 中使用 XML 的映射？](http://go.microsoft.com/fwlink/?LinkID=130288).

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件支持绑定到单个数据字段 （简单数据绑定）。 <xref:Microsoft.Office.Tools.Excel.ListObject>控件可支持复杂数据绑定和重复架构元素映射到单元格上时自动创建。 有关详细信息，请参阅[ListObject 控件](../vsto/listobject-control.md)。

 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件绑定到数据源使用<xref:System.Windows.Forms.Control.DataBindings%2A>属性。 当<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>Visual Studio 自动生成数据集从数据中映射的单元格，并将控件绑定到该数据集添加到工作表单元格。 默认数据绑定属性<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>是<xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Value2%2A>。

 如果绑定数据集中的数据通过任何机制进行了更新<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件会反映出所做的更改。

## <a name="formatting"></a>格式化
 您可以应用相同的格式<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件，可以将应用于<xref:Microsoft.Office.Interop.Excel.Range>。 这包括边框、字体、数字格式和样式。

## <a name="events"></a>事件
 可用于事件<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控制是：

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.SelectionChange>

## <a name="see-also"></a>请参阅
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：向工作表添加 XMLMappedRange 控件](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：将架构映射到 Visual Studio 内部的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
