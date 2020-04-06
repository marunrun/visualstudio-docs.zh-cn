---
title: 自定义编辑器中的文档数据和文档视图 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 04e89194ff09bc273294246cc25718c999daf70f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712135"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>自定义编辑器中的文档数据和文档视图
自定义编辑器由两部分组成：文档数据对象和文档视图对象。 如名称建议，文档数据对象表示要显示的文本数据。 同样，文档视图对象（或"视图"）表示一个或多个窗口，其中用于显示文档数据对象。

## <a name="document-data-object"></a>文档数据对象
 文档数据对象是文本缓冲区中文本的数据表示形式。 它是存储文档文本和其他信息的 COM 对象。 文档数据对象还处理文档持久性，并启用其数据的多个视图。 有关详细信息，请参阅

 <xref:EnvDTE80.Window2.DocumentData%2A>和[文档窗口](../extensibility/internals/document-windows.md)。

 自定义编辑器和设计器可以选择使用<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象或他们自己的自定义缓冲区。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>遵循标准编辑器的简化嵌入模型，支持多个视图，并提供用于管理多个视图的事件接口。

## <a name="document-view-object"></a>文档视图对象
 显示代码和其他文本的窗口称为文档视图或视图。 创建编辑器时，可以选择单个视图，其中文本显示在单个窗口中。 或者，您可以选择多个视图，其中文本显示在多个窗口中。 您的选择取决于您的应用程序。 例如，如果需要并行编辑，请选择多个视图。 每个视图都与集成开发环境 （IDE） 运行的文档表 （RDT） 中的条目相关联。 视图窗口属于项目或<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象。

 如果编辑器支持文档数据对象的多个视图，则文档数据和文档视图对象必须分开。 否则，它们可以分组在一起。 有关详细信息，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

 IDE 通过匹配正在运行的文档表中每个条目的项标识符 （ItemID）来通知有关事件的视图（例如，当包含文档的解决方案关闭时）。 有关此的详细信息，请参阅[运行文档表](../extensibility/internals/running-document-table.md)。

 有两个选项用于为自定义编辑器创建视图。 一个是就地激活模型，其中视图使用 ActiveX 控件或文档数据对象托管在窗口中。 第二个是简化的嵌入模型，其中视图由[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]该模型托管，并<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>实现以处理窗口命令。 有关就地激活模型的信息，请参阅[就地激活](/visualstudio/misc/in-place-activation?view=vs-2015)。 有关简化嵌入模型的信息，请参阅[简化嵌入](../extensibility/simplified-embedding.md)。

## <a name="see-also"></a>请参阅

- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [简化的嵌入](../extensibility/simplified-embedding.md)
- [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)
- [文档锁持有人管理](../extensibility/document-lock-holder-management.md)
- [单选项卡和多选项卡视图](../extensibility/single-and-multi-tab-views.md)
- [保存标准文档](../extensibility/internals/saving-a-standard-document.md)
- [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
- [确定哪个编辑器在项目中打开文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)
