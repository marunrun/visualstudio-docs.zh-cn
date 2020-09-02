---
title: 如何：以编程方式保护工作簿
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: ee7444c63c2d774e9b22ea612049f09429729c79
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537626"
---
# <a name="how-to-programmatically-protect-workbooks"></a>如何：以编程方式保护工作簿
  您可以保护 Microsoft Office Excel 工作簿，使用户不能添加或删除工作表，也不能以编程方式取消保护工作簿。 您可以选择指定一个密码，指出您是否希望 (受保护的结构，以使用户不能在) 周围移动工作表，并指示是否要保护工作簿的 windows。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 保护工作簿不会阻止用户编辑单元格。 若要保护数据，必须保护工作表。 有关详细信息，请参阅 [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)。

 下面的代码示例使用变量来包含从用户获取的密码。

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>保护属于文档级自定义项的工作簿

### <a name="to-protect-a-workbook"></a>保护工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> 工作簿的方法并包含密码。 若要使用下面的代码示例，请在类中运行它 `ThisWorkbook` ，而不是在 sheet 类中运行。

     [!code-csharp[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#10)]
     [!code-vb[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#10)]

### <a name="to-unprotect-a-workbook"></a>取消保护工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A> 方法，并在需要时传递密码。 若要使用下面的代码示例，请在类中运行它 `ThisWorkbook` ，而不是在 sheet 类中运行。

     [!code-csharp[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#11)]
     [!code-vb[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#11)]

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>使用应用程序级外接程序保护工作簿

### <a name="to-protect-a-workbook"></a>保护工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A> 工作簿的方法并包含密码。 此代码示例使用活动工作簿。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#6)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#6)]

### <a name="to-unprotect-a-workbook"></a>取消保护工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A> 活动工作簿的方法，并在需要时传递密码。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#7)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#7)]

## <a name="see-also"></a>另请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
