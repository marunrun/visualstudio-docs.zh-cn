---
title: 如何：以编程方式在 Word 文档中插入文本
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, inserting text in documents
- text [Office development in Visual Studio], inserting in documents
- ranges, replacing text in documents
- documents [Office development in Visual Studio], inserting text
- text [Office development in Visual Studio], replacing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: aef597099964333771fd488e0541b4ea4daf4553
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85541500"
---
# <a name="how-to-programmatically-insert-text-into-word-documents"></a>如何：以编程方式在 Word 文档中插入文本
  向 Microsoft Office Word 文档中插入文本主要有三种方式：

- 在范围中插入文本。

- 将范围中的文本替换为新文本。

- 使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Selection> 方法在光标或所选位置处插入文本。

> [!NOTE]
> 你还可以将文本插入到内容控件和书签中。 有关详细信息，请参阅 [内容控件](../vsto/content-controls.md) 和 [书签控件](../vsto/bookmark-control.md)。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="insert-text-in-a-range"></a>在范围中插入文本
 使用 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 属性在文档中插入文本。

### <a name="to-insert-text-in-a-range"></a>若要在范围中插入文本

1. 在文档开头指定一个范围，并插入文本 **New Text**。

     下面的代码示例可用于文档级自定义项。

     [!code-vb[Trin_VstcoreWordAutomation#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#51)]
     [!code-csharp[Trin_VstcoreWordAutomation#51](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#51)]

     以下代码示例可用于 VSTO 外接程序。 此代码运用了活动文档。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#51)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#51](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#51)]

2. 选择 <xref:Microsoft.Office.Interop.Word.Range> 对象，该对象已从一个字符长度扩展到了插入文本的长度。

     [!code-vb[Trin_VstcoreWordAutomation#52](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#52)]
     [!code-csharp[Trin_VstcoreWordAutomation#52](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#52)]

## <a name="replace-text-in-a-range"></a>替换范围中的文本
 如果指定的范围包含文本，则该范围中的所有文本将被插入的文本替换。

### <a name="to-replace-text-in-a-range"></a>若要替换范围中的文本

1. 创建一个 <xref:Microsoft.Office.Interop.Word.Range> 对象，该对象包含文档中的前 12 个字符。

     下面的代码示例可用于文档级自定义项。

     [!code-vb[Trin_VstcoreWordAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#53)]
     [!code-csharp[Trin_VstcoreWordAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#53)]

     以下代码示例可用于 VSTO 外接程序。 此代码运用了活动文档。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#53)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#53](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#53)]

2. 将这些字符替换为字符串 **New Text**。

     [!code-vb[Trin_VstcoreWordAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#54)]
     [!code-csharp[Trin_VstcoreWordAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#54)]

3. 选择范围。

     [!code-vb[Trin_VstcoreWordAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#55)]
     [!code-csharp[Trin_VstcoreWordAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#55)]

## <a name="insert-text-using-typetext"></a>使用 TypeText 插入文本
 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> 方法可在所选位置处插入文本。 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> 的行为有所不同，具体取决于用户计算机上设置的选项。 以下过程中的代码声明了一个 <xref:Microsoft.Office.Interop.Word.Selection> 对象变量，如果 **Overtype** 选项已打开，则会将其关闭。 如果 **Overtype** 选项已激活，则关闭旁的任何文本将被覆盖。

### <a name="to-insert-text-using-the-typetext-method"></a>若要使用 TypeText 方法插入文本

1. 声明一个 <xref:Microsoft.Office.Interop.Word.Selection> 对象变量。

    [!code-vb[Trin_VstcoreWordAutomation#57](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#57)]
    [!code-csharp[Trin_VstcoreWordAutomation#57](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#57)]

2. 如果 **Overtype** 选项已打开，请将其关闭。

    [!code-vb[Trin_VstcoreWordAutomation#58](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#58)]
    [!code-csharp[Trin_VstcoreWordAutomation#58](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#58)]

3. 测试当前选择项是否未插入点。

    如果是，此代码将使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A>插入一个句子，然后使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeParagraph%2A> 方法插入段落标记。

    [!code-vb[Trin_VstcoreWordAutomation#59](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#59)]
    [!code-csharp[Trin_VstcoreWordAutomation#59](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#59)]

4. **ElseIf** 块中的代码用于测试选择项是否为正常选择项。 如果是，则另一个 **If** 块将测试 **ReplaceSelection** 选项是否已打开。 如果是，该代码将使用选择项的 <xref:Microsoft.Office.Interop.Word.Selection.Collapse%2A> 方法将选择项折叠为文本所选块起始处的插入点。 插入文本和段落标记。

    [!code-vb[Trin_VstcoreWordAutomation#60](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#60)]
    [!code-csharp[Trin_VstcoreWordAutomation#60](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#60)]

5. 如果选择项不是所选文本的插入点或块，则 **Else** 块中的代码将不会执行任何操作。

    [!code-vb[Trin_VstcoreWordAutomation#61](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#61)]
    [!code-csharp[Trin_VstcoreWordAutomation#61](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#61)]

   你还可以使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeBackspace%2A> 对象的方法 <xref:Microsoft.Office.Interop.Word.Selection> ，该方法模仿键盘上 **Backspace** 键的功能。 但是，当涉及到插入和操作文本时，<xref:Microsoft.Office.Interop.Word.Range> 对象将提供更多控件。

   以下示例显示了完整的代码。 若要使用此示例，请运行项目中的 `ThisDocument` 或 `ThisAddIn` 类的代码。

   [!code-vb[Trin_VstcoreWordAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#56)]
   [!code-csharp[Trin_VstcoreWordAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#56)]

## <a name="see-also"></a>另请参阅
- [如何：以编程方式在文档中设置文本格式](../vsto/how-to-programmatically-format-text-in-documents.md)
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式在文档中扩展范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
