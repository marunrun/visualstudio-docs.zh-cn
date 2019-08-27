---
title: 如何：以编程方式从工作簿中删除工作表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9ecc39e72a336c390c85f1caf2c80c6643acbb61
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63412543"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>如何：以编程方式从工作簿中删除工作表
  可以删除工作簿中的任意工作表。 若要删除工作表，请使用该工作表主机项或通过使用工作簿的表集合访问该工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>使用工作表主机项
 如果在设计时将工作表添加到了文档级自定义项，请使用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> 方法来删除指定的工作表。 下列代码通过直接引用工作表主机项从工作簿中删除工作表。

> [!IMPORTANT]
> 此代码仅在使用下列任意项目模板创建的项目中运行：
>
> - Excel 2013 工作簿
> - Excel 2013 模板
> - Excel 2010 工作簿
> - Excel 2010 模板
>
>   如果你想要在任何其他类型的项目中执行此任务，则必须添加对的引用**Microsoft.Office.Interop.Excel**程序集，然后必须使用该程序集的类来打开工作簿或删除工作表。 有关详细信息，请参阅[如何：面向 Office 应用程序可以通过主互操作程序集](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)并[Excel 2010 主互操作程序集引用](http://go.microsoft.com/fwlink/?LinkId=189585)。

### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>使用工作表主机项删除工作表

1. 调用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> 的 `Sheet1`方法。

     [!code-csharp[Trin_VstcoreExcelAutomation#17](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomation#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#17)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合
 在下列情况中通过 Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Sheets> 集合访问工作表：

- 想要删除 VSTO 外接程序中的工作表。

- 想要删除的工作表是在运行时文档级自定义项中创建的。

  下面的代码引用的索引号的表，从而删除该工作表从工作簿**表**集合。 此代码假定以编程方式创建了一个新工作表。

> [!IMPORTANT]
> 如果你想要在任何其他类型的项目中执行此任务，则必须添加对的引用**Microsoft.Office.Interop.Excel**程序集，然后必须使用该程序集的类来打开工作簿或删除工作表。 有关详细信息，请参阅[如何：面向 Office 应用程序可以通过主互操作程序集](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)并[Excel 2010 主互操作程序集引用](http://go.microsoft.com/fwlink/?LinkId=189585)。

### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合删除工作表

1. 调用 <xref:Microsoft.Office.Interop.Excel.Sheets> 集合的 <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> 方法。

     [!code-csharp[Trin_VstcoreExcelAutomation#18](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#18)]
     [!code-vb[Trin_VstcoreExcelAutomation#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#18)]

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [如何：以编程方式移动工作簿内的工作表](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [如何：以编程方式选择工作表](../vsto/how-to-programmatically-select-worksheets.md)
- [如何：以编程方式将新工作表添加到工作簿](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [工作表主机项](../vsto/worksheet-host-item.md)
- [对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
