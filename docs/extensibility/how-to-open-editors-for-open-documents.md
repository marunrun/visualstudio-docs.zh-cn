---
title: 如何：打开打开文档的编辑器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d0986573ac0d53427f6490370be2bfa1c4cbe7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710915"
---
# <a name="how-to-open-editors-for-open-documents"></a>如何：打开打开文档的编辑器
在项目打开文档窗口之前，项目首先必须确定该文件是否已在另一个编辑器的文档窗口中打开。 该文件可以在特定于项目的编辑器中打开，也可以在 中注册的标准编辑器之一打开[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

## <a name="open-a-project-specific-editor"></a>打开特定于项目的编辑器
 使用以下过程为已打开的文件打开特定于项目的编辑器。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>为打开的文件打开特定于项目的编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 方法。

    如果适用，此调用返回指向文档层次结构、层次结构项和窗口框架的指针。

2. 如果文档处于打开状态，则项目必须检查是否存在文档数据对象，或者文档视图对象是否也存在。

   - 如果存在文档视图对象，并且此视图用于其他层次结构或层次结构项，则项目使用指向视图窗口框架的指针重新显示现有窗口。

   - 如果存在文档视图对象，并且此视图适用于同一层次结构和层次结构项，则如果项目可以附加到基础文档数据对象，则可以打开第二个视图。 否则，项目应使用指向视图窗口框架的指针重新显示现有窗口。

   - 如果仅存在文档数据对象，则项目应确定是否可以将文档数据对象用于其视图。 如果文档数据对象兼容，则完成[打开特定于项目的编辑器](../extensibility/how-to-open-project-specific-editors.md)中讨论的步骤。

     如果文档数据对象不兼容，则应向用户显示指示文件当前正在使用的错误。 此错误应仅在瞬时情况下显示，例如当用户尝试使用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]核心文本编辑器以外的编辑器打开文件的同时编译文件时。 核心文本编辑器可以与编译器共享文档数据对象。

3. 如果文档由于没有文档数据对象或文档视图对象而未打开，则完成["打开特定于项目的编辑器"](../extensibility/how-to-open-project-specific-editors.md)中的步骤。

## <a name="open-a-standard-editor"></a>打开标准编辑器
 使用以下过程为已打开的文件打开标准编辑器。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>为打开的文件打开标准编辑器

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>。

     此方法首先通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>验证文档尚未打开。 如果文档已打开，则其编辑器窗口将重新显示。

2. 如果文档未打开，则完成["如何打开标准编辑器](../extensibility/how-to-open-standard-editors.md)"中的步骤。

## <a name="see-also"></a>请参阅
- [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开特定于项目的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
