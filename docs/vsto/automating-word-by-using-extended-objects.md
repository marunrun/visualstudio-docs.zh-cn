---
title: 使用扩展对象实现 Word 自动化
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], automating
- extended objects [Office development in Visual Studio], Word
- automation [Office development in Visual Studio], Word
- host items [Office development in Visual Studio], Word
- automating Word
- controls [Office development in Visual Studio], Word host controls
- host controls, Word
- host controls [Office development in Visual Studio], Word
- Word [Office development in Visual Studio], host controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 083fe8cdd3bf9d0e4de4809aacfb78b537e4ed8e
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255536"
---
# <a name="automate-word-by-using-extended-objects"></a>使用扩展对象实现 Word 自动化
  当在 Visual Studio 中开发 Word 解决方案时，可以使用解决方案中的 *宿主项* 和 *宿主控件*。 这些对象可扩展 Word 对象模型（即由 Word 主互操作程序集公开的对象模型）中的一些常用对象，例如 <xref:Microsoft.Office.Interop.Word.Document> 和 <xref:Microsoft.Office.Interop.Word.ContentControl> 对象。 扩展对象的行为类似于其所基于的 Word 对象，但它们可以将其他事件和数据绑定功能添加到对象。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 虽然使用宿主项和宿主控件所在的上下文对于每种类型的解决方案有所不同，但它们均可用于 VSTO 外接程序和文档级自定义项。 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

## <a name="document-host-item"></a>文档宿主项
 Word 项目可授予你访问 <xref:Microsoft.Office.Tools.Word.Document> 宿主项的权限。 <xref:Microsoft.Office.Tools.Word.Document> 宿主项还可充当其他控件（包括宿主控件和 Windows 窗体控件）的容器，并且还可保留有关其界面上的控件的信息。 <xref:Microsoft.Office.Tools.Word.Document> 宿主项还提供了大部分与 <xref:Microsoft.Office.Interop.Word.Document> 类相同的成员，该类是 Word 对象模型中的对应类。

 有关详细信息，请参阅[文档主机项](../vsto/document-host-item.md)。

## <a name="word-host-controls"></a>Word 宿主控件
 有多个可用于 Word 的宿主控件，这些控件有助于你创建、组织和自动处理文档。 它们的大部分功能包含了导入、呈现和保护数据。 这些宿主控件可提供本机 Word 对象模型中的相应控件所无法提供的事件和数据绑定功能。

 在文档级项目中，可以在设计时向文档中添加宿主控件，或在运行时添加内容控件和书签控件。 在 VSTO 外接程序项目中，可以在运行时向任何打开的文档中添加内容控件和书签控件。

 有关可以在 Word 项目中使用的宿主控件的详细信息，请参阅以下主题：

- [内容控件](../vsto/content-controls.md)

- [Bookmark 控件](../vsto/bookmark-control.md)

- [XMLNode 控件](../vsto/xmlnode-control.md)

- [XMLNodes 控件](../vsto/xmlnodes-control.md)

## <a name="see-also"></a>请参阅
- [如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)
- [如何：向 Word 文档添加书签控件](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [如何：向 Word 文档添加 XMLNode 控件](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)
- [如何：将 XMLNodes 控件添加到 Word 文档](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)
- [如何：调整书签控件的大小](../vsto/how-to-resize-bookmark-controls.md)
- [演练：使用内容控件创建模板](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)
- [演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)
- [演练：为书签创建快捷菜单](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [Word 解决方案](../vsto/word-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
