---
title: 如何：打开项目特定的编辑器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 22106ea09f86e3d61fe7aaa6e86e6e99c002f32d
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905810"
---
# <a name="how-to-open-project-specific-editors"></a>如何：打开项目特定的编辑器
如果项目打开的项文件在本质上绑定到该项目的特定编辑器，则该项目必须使用特定于项目的编辑器打开该文件。 此文件不能被委派到 IDE 用于选择编辑器的机制。 例如，您可以使用特定于项目的编辑器选项来指定特定的位图编辑器，该编辑器可识别您的项目特有的文件中的信息，而不是使用标准的位图编辑器。

 IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 在确定文件应由特定项目打开时调用方法。 有关详细信息，请参阅[使用 "打开文件" 命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 使用以下准则来实现 `OpenItem` 方法，使你的项目使用特定于项目的编辑器打开文件。

## <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>使用特定于项目的编辑器实现 OpenItem 方法

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> 方法（ `RDT_EditLock` ）以确定文件（文档数据对象）是否已打开。

    > [!NOTE]
    > 有关文档数据和文档视图对象的详细信息，请参阅[文档数据和自定义编辑器中的文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)。

2. 如果文件已打开，请通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 方法并为参数指定 IDO_ActivateIfOpen 的值来 resurface 文件 `grfIDO` 。

     如果文件已打开，并且文档由项目而不是调用项目所拥有，则会向用户显示一条警告，指示正在打开的编辑器来自其他项目。 然后，将显示 "文件" 窗口。

3. 如果您的文本缓冲区（文档数据对象）已打开，并且您想要将另一个视图附加到它，则您负责连接该视图。 从项目中实例化视图（文档视图对象）的建议方法如下：

    1. 对 `QueryService` 服务调用 <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> 以获取指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> 。

    2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 方法来创建文档视图类的实例。

4. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> 方法，并指定文档视图对象。

     此方法在文档窗口中显示文档视图对象。

5. 对或方法执行适当的调用 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> 。

     此时，视图应完全初始化并可以打开。

6. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 方法以显示并打开该视图。

## <a name="see-also"></a>另请参阅
- [打开并保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
- [如何：打开打开的文档的编辑器](../extensibility/how-to-open-editors-for-open-documents.md)
