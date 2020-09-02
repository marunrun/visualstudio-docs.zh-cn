---
title: 如何：以编程方式在文档中检查拼写
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], checking spelling
- spelling checker, documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 93ba9d9907135952f7408652bfb36f440d23138d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537847"
---
# <a name="how-to-programmatically-check-spelling-in-documents"></a>如何：以编程方式在文档中检查拼写
  若要检查文档中的拼写，请使用 <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> 方法。 此方法返回一个布尔值，该值指示所提供的参数是否拼写正确。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-check-spelling-and-display-results-in-a-message-box"></a>检查拼写并在消息框中显示结果

1. 调用 <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> 方法并向其传递一系列文本以检查拼写错误。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#113](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#113)]
     [!code-csharp[Trin_VstcoreWordAutomation#113](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#113)]

## <a name="see-also"></a>另请参阅
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
