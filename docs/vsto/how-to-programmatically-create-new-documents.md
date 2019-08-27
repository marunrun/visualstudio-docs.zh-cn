---
title: 如何：以编程方式创建新的文档
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], custom document
- Word [Office development in Visual Studio], creating documents
- documents [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4940b5f5064fdb47439ad6b38b855785ae06c781
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62575125"
---
# <a name="how-to-programmatically-create-new-documents"></a>如何：以编程方式创建新的文档
  当以编程方式创建文档时，新文档是一个本机 <xref:Microsoft.Office.Interop.Word.Document> 对象。 此对象不具有 <xref:Microsoft.Office.Tools.Word.Document> 主机项的其他事件和数据绑定功能。 有关详细信息，请参阅[主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 开发文档级项目时，不能以编程方式将 <xref:Microsoft.Office.Tools.Word.Document> 主机项添加到你的项目。 在 VSTO 外接程序项目中，可在运行时将任意 <xref:Microsoft.Office.Interop.Word.Document> 对象转换为 <xref:Microsoft.Office.Tools.Word.Document> 主机项。 有关详细信息，请参阅[扩展 Word 文档和 Excel 工作簿中运行时在 VSTO 加载项](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="to-create-a-new-document-based-on-the-normal-template"></a>基于 Normal 模板创建新文档

- 使用 <xref:Microsoft.Office.Interop.Word.Documents> 集合的 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 方法来创建基于 Normal 模板的新文档。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#1)]
     [!code-csharp[Trin_VstcoreWordAutomation#1](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#1)]

## <a name="use-custom-templates"></a>使用自定义模板
 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A>方法具有一个可选*模板*参数以创建一个新的文档基于 Normal 模板以外的模板。 你必须提供模板的文件名称和完全限定路径。

### <a name="to-create-a-new-document-based-on-a-custom-template"></a>基于自定义模板创建新文档

- 调用 <xref:Microsoft.Office.Interop.Word.Documents> 集合的 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 方法，并指定模板的路径。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#2)]
     [!code-csharp[Trin_VstcoreWordAutomation#2](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#2)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
