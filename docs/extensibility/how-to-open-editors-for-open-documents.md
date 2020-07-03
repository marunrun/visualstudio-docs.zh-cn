---
title: 如何：打开打开的文档的编辑器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f67a7fad5944e82087f520508ef9f4a66b7109d
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905818"
---
# <a name="how-to-open-editors-for-open-documents"></a>如何：打开打开的文档的编辑器
在项目打开文档窗口之前，项目首先必须确定是否已在另一个编辑器的文档窗口中打开该文件。 此文件可以在特定于项目的编辑器中打开，也可以在向注册的某个标准编辑器中打开 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="open-a-project-specific-editor"></a>打开特定于项目的编辑器
 使用以下过程为已打开的文件打开特定于项目的编辑器。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>为打开的文件打开特定于项目的编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 方法。

    如果适合，此调用将返回指向文档层次结构项和窗口框架的指针。

2. 如果文档处于打开状态，则项目必须进行检查以确定是否仅存在文档数据对象，或者是否也存在文档视图对象。

   - 如果存在文档视图对象，而此视图用于不同的层次结构或层次结构项，则项目将使用指向视图窗口框架的指针来 resurface 现有窗口。

   - 如果某个文档视图对象存在并且此视图用于相同的层次结构和层次结构项，则项目可以打开第二个视图（如果它可以附加到基础文档数据对象）。 否则，项目应使用指向视图窗口框架的指针 resurface 现有窗口。

   - 如果只有文档数据对象存在，则项目应确定它是否可以使用文档数据对象查看其视图。 如果文档数据对象兼容，请完成[打开项目特定编辑器](../extensibility/how-to-open-project-specific-editors.md)中所述的步骤。

     如果文档数据对象不兼容，则应向用户显示错误，指示该文件当前正在使用中。 此错误应仅在暂时性情况下显示，例如，当用户尝试使用核心文本编辑器之外的编辑器打开文件时，正在编译文件时 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 核心文本编辑器可以与编译器共享文档数据对象。

3. 如果文档因为没有文档数据对象或文档视图对象而未打开，请完成[打开项目特定编辑器](../extensibility/how-to-open-project-specific-editors.md)中的步骤。

## <a name="open-a-standard-editor"></a>打开标准编辑器
 使用以下过程为已打开的文件打开标准编辑器。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>为打开的文件打开标准编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>。

     此方法首先通过调用验证该文档是否尚未打开 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 。 如果文档已打开，则其编辑器窗口将为 resurfaced。

2. 如果文档未打开，请完成[如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)中的步骤。

## <a name="see-also"></a>另请参阅
- [打开并保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开项目特定的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
