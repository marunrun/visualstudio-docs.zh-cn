---
title: 以编程方式保护文档和文档的某些部分
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document protection
- documents [Office development in Visual Studio], document protection
- Word documents, protection
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4654a2c218470e0d5e2a1ddd54a88de5c4546f7b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537834"
---
# <a name="how-to-programmatically-protect-documents-and-parts-of-documents"></a>如何：以编程方式保护文档和文档的某些部分
  你可以为 Microsoft Office Word 文档添加保护，以防止用户对文档进行任何编辑操作。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 还可以将文档的特定区域标记为例外，使指定用户只能编辑文档的这些区域。 例如，你可能希望保护整个文档，但某个特定的书签除外。 可选择添加密码，这样一来，除非用户知道此密码，否则无法删除文档保护。

> [!NOTE]
> 下面的示例未使用密码保护；但是，在添加文档保护时，你可能想考虑使用密码。 有关详细信息，请参阅[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的文档保护程序示例。

 你也可以使用内容控件来保护文档的各个部分。 有关详细信息，请参阅[如何：使用内容控件保护文档的各个部分](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)。

## <a name="protect-a-document-that-is-part-of-a-document-level-customization"></a>保护属于文档级自定义项的文档

### <a name="to-protect-a-document-that-is-part-of-a-document-level-customization"></a>若要保护属于文档级自定义项的文档

1. 调用项目中 <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> 类的 `ThisDocument` 方法。

     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]

### <a name="to-exclude-a-bookmark-control-from-document-protection"></a>从文档保护中排除 Bookmark 控件

1. 使用 <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> 方法保护整个文档。

     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]

2. 从文档保护中排除 `Bookmark1` 。

     [!code-vb[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#112)]
     [!code-csharp[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#112)]

### <a name="compile-the-code"></a>编译代码
 若要使用这些代码示例，请从项目内的 `ThisDocument` 类中运行这些示例。 这些代码示例假定在出现此代码的文档中有一个名为 <xref:Microsoft.Office.Tools.Word.Bookmark> 的现有 `Bookmark1` 控件。

## <a name="protect-a-document-by-using-a-vsto-add-in"></a>使用 VSTO 外接程序保护文档

### <a name="to-protect-a-document-by-using-an-application-level-vsto-add-in"></a>使用应用程序级 VSTO 外接程序保护文档

1. 调用要保护的 <xref:Microsoft.Office.Interop.Word._Document.Protect%2A> 的 <xref:Microsoft.Office.Interop.Word.Document> 方法。

     下面的代码示例将保护活动文档。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#111)]

## <a name="see-also"></a>另请参阅
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)
- [如何：允许代码在具有受限权限的文档的后台运行](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [如何：向 Word 文档添加书签控件](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
