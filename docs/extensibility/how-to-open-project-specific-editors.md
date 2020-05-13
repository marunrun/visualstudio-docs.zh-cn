---
title: 如何：打开特定于项目的编辑器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3cb6e360a38d64de4976f83b0167d47dc03fbc87
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710843"
---
# <a name="how-to-open-project-specific-editors"></a>如何：打开特定于项目的编辑器
如果项目正在打开的项文件本质上是绑定到该项目的特定编辑器的，则项目必须使用特定于项目的编辑器打开该文件。 文件不能委派给 IDE 选择编辑器的机制。 例如，可以使用特定于项目的编辑器来指定特定的位图编辑器，该编辑器可识别项目中唯一的信息，而不是使用标准位图编辑器。

 当 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>确定特定项目应打开文件时，它调用该方法。 有关详细信息，请参阅[使用打开文件命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 使用以下准则实现`OpenItem`使用特定于项目的编辑器使项目打开文件的方法。

## <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>使用特定于项目的编辑器实现 OpenItem 方法

1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>方法`RDT_EditLock`（ ） 以确定文件（文档数据对象）是否已打开。

    > [!NOTE]
    > 有关文档数据和文档视图对象的详细信息，请参阅[自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)。

2. 如果文件已打开，则通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>方法并为`grfIDO`参数指定IDO_ActivateIfOpen值来重新显示该文件。

     如果文件处于打开状态，并且文档归调用项目以外的项目所有，则向用户显示一条警告，指出正在打开的编辑器来自另一个项目。 然后，文件窗口将浮出水面。

3. 如果文本缓冲区（文档数据对象）已打开，并且要附加另一个视图，则负责连接该视图。 建议从项目中实例化视图（文档视图对象）的方法如下：

    1. 调用`QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry>服务以获取指向接口的<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2>指针。

    2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>方法以创建文档视图类的实例。

4. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>方法，指定文档视图对象。

     此方法将文档视图对象设置在文档窗口中。

5. 对 或<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A><xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A>方法执行适当的调用。

     此时，视图应完全初始化并准备打开。

6. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>方法以显示并打开视图。

## <a name="see-also"></a>请参阅
- [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
- [如何：打开打开文档的编辑器](../extensibility/how-to-open-editors-for-open-documents.md)
