---
title: 自定义编辑器中的文档数据和文档视图 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2aa8779a069f4b001743326470f69f3cb35a8c10
ms.sourcegitcommit: 97623fd6190c43fed0d2ee7af92b01c375282622
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73568881"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>自定义编辑器中的文档数据和文档视图
自定义编辑器由两部分组成：文档数据对象和文档视图对象。 顾名思义，文档数据对象表示要显示的文本数据。 同样，文档视图对象（或 "视图"）表示要在其中显示文档数据对象的一个或多个窗口。

## <a name="document-data-object"></a>文档数据对象
 文档数据对象是文本缓冲区中文本的数据表示形式。 它是存储文档文本和其他信息的 COM 对象。 文档数据对象还处理文档持久性，并启用其数据的多个视图。 有关详细信息，请参阅

 <xref:EnvDTE80.Window2.DocumentData%2A> 和[文档窗口](../extensibility/internals/document-windows.md)。

 自定义编辑器和设计器可以选择使用 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对象或其自己的自定义缓冲区。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 遵循标准编辑器的简化嵌入模型，支持多个视图，并提供用于管理多个视图的事件接口。

## <a name="document-view-object"></a>文档视图对象
 显示代码和其他文本的窗口称为 "文档视图" 或 "视图"。 创建编辑器时，可以选择单个视图，其中的文本显示在单个窗口中。 也可以选择多个视图，其中的文本显示在多个窗口中。 你的选择取决于你的应用程序。 例如，如果需要并排编辑，则可以选择多个视图。 每个视图都与集成开发环境（IDE）运行文档表（RDT）中的项相关联。 视图窗口属于项目或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 对象。

 如果编辑器支持文档数据对象的多个视图，则文档数据和文档视图对象必须是独立的。 否则，可以将它们组合在一起。 有关详细信息，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

 IDE 通过为正在运行的文档表中的每个条目匹配项标识符（ItemID）来通知有关事件（例如，包含文档的解决方案）的视图。 有关此内容的详细信息，请参阅[运行文档表](../extensibility/internals/running-document-table.md)。

 有两个选项可用于创建自定义编辑器的视图。 一种是就地激活模型，其中的视图承载于使用 ActiveX 控件或文档数据对象的窗口中。 第二个是简化的嵌入模型，其中视图由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 承载，并实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 来处理窗口命令。 有关就地激活模型的信息，请参阅[就地激活](/visualstudio/misc/in-place-activation?view=vs-2015)。 有关简化的嵌入模型的信息，请参阅[简化嵌入](../extensibility/simplified-embedding.md)。

## <a name="see-also"></a>请参阅

- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [简化的嵌入](../extensibility/simplified-embedding.md)
- [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)
- [文档锁持有者管理](../extensibility/document-lock-holder-management.md)
- [单个和多个选项卡视图](../extensibility/single-and-multi-tab-views.md)
- [保存标准文档](../extensibility/internals/saving-a-standard-document.md)
- [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
- [确定在项目中打开文件的编辑器](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)