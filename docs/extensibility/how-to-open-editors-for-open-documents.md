---
title: 如何：打开编辑器中打开的文档提供 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c8342947681bcd8f698c2a646e917b353ec6c9dd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319331"
---
# <a name="how-to-open-editors-for-open-documents"></a>如何：打开编辑器的打开的文档
项目将打开一个文档窗口之前，项目首先必须确定文件是否已打开在另一个编辑器的文档窗口中。 该文件可以为在特定于项目的编辑器中，或者打开或其中一个标准编辑器注册[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

## <a name="open-a-project-specific-editor"></a>打开特定于项目的编辑器
 使用以下过程打开已打开的文件的特定于项目的编辑器。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>若要打开打开的文件的特定于项目的编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 方法。

    如果适用，此调用返回到文档的层次结构、 层次结构项和窗口框架指针。

2. 如果文档处于打开状态，必须检查该项目以查看是否存在仅文档数据对象，或如果文档视图对象也存在。

   - 如果文档视图对象存在，并且此视图是不同的层次结构或层次结构项，project 使用指向该视图的窗口框架的 resurface 现有窗口。

   - 如果文档视图对象存在，并且此视图相同的层次结构和层次结构项，项目可打开第二个视图，如果它可以将附加到基础文档数据对象。 否则，该项目应使用视图的窗口框架的指针来 resurface 现有窗口。

   - 如果只存在文档数据对象，该项目应确定是否可以为其视图使用文档数据对象。 如果文档数据对象是否兼容，完成步骤中所述[特定于项目的编辑器打开](../extensibility/how-to-open-project-specific-editors.md)。

     如果文档数据对象不兼容，则应指示文件正在使用中的用户显示错误。 此错误应仅显示在暂时性情况下，如文件在同一时间在编译时用户尝试打开该文件而不使用编辑器[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]核心文本编辑器。 核心文本编辑器可以共享包含编译器的文档数据对象。

3. 如果文档未打开，因为没有文档数据对象或文档视图对象，请完成中的步骤[特定于项目的编辑器打开](../extensibility/how-to-open-project-specific-editors.md)。

## <a name="open-a-standard-editor"></a>打开标准编辑器
 使用以下过程可打开标准编辑器文件已打开。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>若要打开的标准编辑器打开的文件

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>。

     此方法首先验证，该文档未打开通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>。 如果文档已打开，然后重新呈现其编辑器窗口。

2. 如果文档未打开，然后完成中的步骤[如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)。

## <a name="see-also"></a>请参阅
- [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开项目特定的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
