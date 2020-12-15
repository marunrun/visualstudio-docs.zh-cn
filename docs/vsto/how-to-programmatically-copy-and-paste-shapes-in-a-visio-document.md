---
title: 以编程方式在 Visio 文档中复制和粘贴形状
description: 了解如何以编程方式复制文档的一页上的形状，并将其粘贴到同一文档中的新页中。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- shapes [Office development in Visual Studio], copying and pasting Visio shapes
- Visio [Office development in Visual Studio], copying and pasting Visio shapes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4643d1527d078639e2f2f09add42fff96e345091
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523203"
---
# <a name="how-to-programmatically-copy-and-paste-shapes-in-a-visio-document"></a>如何：以编程方式在 Visio 文档中复制和粘贴形状
  你可以以编程方式复制文档中某一页上的形状，并将其粘贴到同一文档中新的一页。 你可以选择将其粘贴到默认位置（活动窗口的中央），或将其粘贴到与在其原始页相同的坐标位置。

## <a name="copy-and-paste-shapes"></a>复制和粘贴形状
 有关对象模型的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle)、 [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval)、 [Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy)和 [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) 方法以及 [Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNormal](/office/vba/api/Visio.viscutcopypastecodes) 标志的 VBA 参考文档。

### <a name="to-copy-shapes-to-the-center-of-another-page"></a>将形状复制到另一页的中央

- 下面的示例演示如何复制第一页中的形状并将其粘贴到第二页的中央。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#14](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#14)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#14](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#14)]

## <a name="copy-and-paste-shapes-with-the-same-positions"></a>复制和粘贴具有相同位置的形状
 有关对象模型的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle)、 [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval)、 [Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy)和 [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) 方法以及 [Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNoTranslate](/office/vba/api/Visio.viscutcopypastecodes) 标志的 VBA 参考文档。

 如果需要控制粘贴的信息的格式，并 (可以选择) 建立指向源文件的链接 (例如，Microsoft Office Word 文档) ，请使用 PasteSpecial 方法。

### <a name="to-copy-shapes-and-shape-locations-to-another-page"></a>将形状和形状位置复制到另一页

- 下面的示例演示如何复制第一页中的形状并将其粘贴到第二页中与其原始坐标相同的位置。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#15](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#15)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#15](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#15)]

## <a name="see-also"></a>另请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [使用 Visio 形状](../vsto/working-with-visio-shapes.md)
- [如何：以编程方式向 Visio 文档添加形状](../vsto/how-to-programmatically-add-shapes-to-a-visio-document.md)
