---
title: 如何：以编程方式打开现有文档
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening
- Word [Office development in Visual Studio], opening documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eba4d110b06147db384a4d7aafe01c7d9f272ba3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519894"
---
# <a name="how-to-programmatically-open-existing-documents"></a>如何：以编程方式打开现有文档
  <xref:Microsoft.Office.Interop.Word.Documents.Open%2A>方法打开由完全限定的路径和文件名指定的现有 Microsoft Office Word 文档。 此方法返回一个 <xref:Microsoft.Office.Interop.Word.Document> 表示打开的文档的。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-open-a-document"></a>打开文档

- 调用 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 集合的方法 <xref:Microsoft.Office.Interop.Word.Documents> ，并提供文档的路径。

     [!code-vb[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#5)]

## <a name="to-open-a-document-as-read-only"></a>以只读方式打开文档

- 调用 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 方法，提供文档的路径，并在方法调用中将*ReadOnly*参数设置**为 True** 。

     [!code-vb[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#6)]
     [!code-csharp[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#6)]

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 名为*NewDocument.doc*的文档必须存在于驱动器 C 上名为*Test*的目录中。

## <a name="see-also"></a>另请参阅
- [如何：以编程方式创建新文档](../vsto/how-to-programmatically-create-new-documents.md)
- [如何：以编程方式关闭文档](../vsto/how-to-programmatically-close-documents.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
