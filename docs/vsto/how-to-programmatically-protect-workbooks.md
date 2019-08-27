---
title: 如何：以编程方式保护工作簿
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, passwords
- documents [Office development in Visual Studio], document protection
- workbooks, unprotecting
- document protection, removing from workbooks
- document protection, adding to workbooks
- workbooks, protecting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ad45097146a7566f2d043fba5e14265c05dc4d7a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955904"
---
# <a name="how-to-programmatically-protect-workbooks"></a>如何：以编程方式保护工作簿
  你可以保护 Microsoft Office Excel 工作簿，以便用户不能添加或删除工作表，并还以编程方式取消保护工作簿。 （可选） 可以指定一个密码，指示是否希望保护 （因此，用户不能移动表），该结构以及指示是否要保护的工作簿的 windows。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 保护工作簿不会阻止用户编辑单元格。 若要保护的数据，您必须保护工作表。 有关详细信息，请参阅[如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)。

 下面的代码示例使用变量来存放从用户获得的密码。

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>保护属于文档级自定义的工作簿

### <a name="to-protect-a-workbook"></a>若要保护的工作簿

1. 调用<xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A>工作簿的方法，包括密码。 若要使用下面的代码示例，请运行`ThisWorkbook`类，不在表类。

     [!code-csharp[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#10)]
     [!code-vb[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#10)]

### <a name="to-unprotect-a-workbook"></a>若要取消保护工作簿

1. 调用<xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A>方法，如果需要传递密码。 若要使用下面的代码示例，请运行`ThisWorkbook`类，不在表类。

     [!code-csharp[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#11)]
     [!code-vb[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#11)]

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>通过使用应用程序级外接程序来保护工作簿

### <a name="to-protect-a-workbook"></a>若要保护的工作簿

1. 调用<xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A>工作簿的方法，包括密码。 此代码示例使用活动的工作簿。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#6)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#6)]

### <a name="to-unprotect-a-workbook"></a>若要取消保护工作簿

1. 调用<xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A>活动工作簿，如果需要将密码传递方法。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#7)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#7)]

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
