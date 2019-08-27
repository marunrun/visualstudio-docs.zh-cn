---
title: 如何：以编程方式搜索中工作表范围内的文本
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, searching
- text [Office development in Visual Studio], searching in worksheets
- text searches, worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3e0befc61b39030bd7144cef10b54e70dc71e33a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419550"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>如何：以编程方式在工作表范围内搜索文本
  <xref:Microsoft.Office.Interop.Excel.Range.Find%2A>方法的<xref:Microsoft.Office.Interop.Excel.Range>对象可用于搜索的范围内的文本。 此文本也可以是任何错误字符串，如出现在工作表单元格`#NULL!`或`#VALUE!`。 有关错误字符串的详细信息，请参阅[单元格错误值](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values)。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 下面的示例名为某个范围中搜索`Fruits`并修改的单元格包含单词"apples"的字体。 此过程还使用<xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A>方法，它使用先前设置搜索设置重复搜索。 指定在其搜索之后, 该单元格和<xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A>方法处理其余部分。

> [!NOTE]
> <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A>后到达范围末尾的操作方法的搜索会返回到搜索范围的开头。 你的代码必须确保搜索不会不环绕在周围的无限循环。 示例过程显示了一种方法来处理这种使用<xref:Microsoft.Office.Interop.Excel.Range.Address%2A>属性。

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：在 Excel 外接程序中使用 Find 方法？](http://go.microsoft.com/fwlink/?LinkID=130294).

## <a name="to-search-for-text-in-a-worksheet-range"></a>若要在工作表范围内搜索文本

1. 用于跟踪整个范围、 找到的第一个范围和找到的当前范围变量声明。

    [!code-csharp[Trin_VstcoreExcelAutomation#58](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#58)]
    [!code-vb[Trin_VstcoreExcelAutomation#58](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#58)]

2. 搜索第一个匹配项，指定要搜索后的单元格以外的所有参数。

    [!code-csharp[Trin_VstcoreExcelAutomation#59](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#59)]
    [!code-vb[Trin_VstcoreExcelAutomation#59](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#59)]

3. 继续搜索，只要有匹配项。

    [!code-csharp[Trin_VstcoreExcelAutomation#60](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#60)]
    [!code-vb[Trin_VstcoreExcelAutomation#60](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#60)]

4. 比较找到的第一个范围 (`firstFind`) 到**Nothing**。 如果`firstFind`找到的范围不包含任何值，则代码将存储消失 (`currentFind`)。

    [!code-csharp[Trin_VstcoreExcelAutomation#61](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#61)]
    [!code-vb[Trin_VstcoreExcelAutomation#61](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#61)]

5. 如果找到的范围的地址与找到的第一个范围的地址相匹配，则退出循环。

    [!code-csharp[Trin_VstcoreExcelAutomation#62](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#62)]
    [!code-vb[Trin_VstcoreExcelAutomation#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#62)]

6. 设置查找范围的外观。

    [!code-csharp[Trin_VstcoreExcelAutomation#63](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#63)]
    [!code-vb[Trin_VstcoreExcelAutomation#63](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#63)]

7. 执行另一个搜索。

    [!code-csharp[Trin_VstcoreExcelAutomation#64](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#64)]
    [!code-vb[Trin_VstcoreExcelAutomation#64](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#64)]

   以下示例显示完整的方法。

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreExcelAutomation#57](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#57)]
 [!code-vb[Trin_VstcoreExcelAutomation#57](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#57)]

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式引用在代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
