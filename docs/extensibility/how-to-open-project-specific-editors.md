---
title: 如何：打开项目特定的编辑器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2e85913f6eead81bcbc2424ef1087f64a3f2446e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319241"
---
# <a name="how-to-open-project-specific-editors"></a>如何：打开项目特定的编辑器
如果要打开的项目项文件本质上绑定到该项目的特定编辑器中，项目必须使用特定于项目的编辑器打开文件。 该文件不能被委派到 IDE 的机制，用于选择一个编辑器。 例如，而不是使用标准的位图编辑器，您可以使用此项目特定的编辑器选项来指定一个特定的位图编辑器，识别仅适用于你的项目文件中的信息。

 IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>方法时它会确定应由特定项目打开的文件。 有关详细信息，请参阅[通过使用打开文件命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 使用以下指导原则来实现`OpenItem`方法，以使您通过使用特定于项目的编辑器打开文件的项目。

## <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>若要使用特定于项目的编辑器实现 OpenItem 方法

1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>方法 (`RDT_EditLock`) 来确定文件 （文档数据对象） 是否已打开。

    > [!NOTE]
    > 有关文档数据和文档视图对象的详细信息，请参阅[文档自定义编辑器中的数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)。

2. 如果该文件已打开，通过调用 resurface 文件<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>方法，并将值指定为 IDO_ActivateIfOpen`grfIDO`参数。

     如果文件已打开，并且该文档拥有的而不是调用项目的项目，将向正在打开的编辑器是从另一个项目的用户显示一条警告。 然后显示文件窗口中。

3. 如果在文本缓冲区 （文档数据对象） 已打开并且你想要将另一个视图附加到它，您负责挂接该视图。 从项目中，实例化视图 （文档视图对象） 的建议的方法是按如下所示：

    1. 调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry>服务以获取一个指向<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2>接口。

    2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>方法来创建文档视图类的实例。

4. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>方法，指定您的文档视图对象。

     此方法站点在文档窗口中的文档视图对象。

5. 执行到相应的调用<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A>或<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A>方法。

     此时，该视图应该是完全初始化并准备打开。

6. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>方法来显示和打开该视图。

## <a name="see-also"></a>请参阅
- [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
- [如何：打开编辑器的打开的文档](../extensibility/how-to-open-editors-for-open-documents.md)